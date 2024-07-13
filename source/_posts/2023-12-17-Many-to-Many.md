---
title: Many to Many
date: 2023-12-17 10:09:25
toc: true  
categories:  
- Spring Boot 3


---

#Many to Many

### DAO

```java
public interface AppDAO {
    void save(Instructor theInstructor);
    Instructor findInstructorById(int theId);
    void deleteInstructorById(int theId);
  
    InstructorDetail findInstructorDetailById(int theId);
    void deleteInstructorDetailById(int theId);
  
    List<Course> findCourseByInstructorId(int theId);
    Instructor findInstructorByIdJoinFetch(int theId);
  
    void update(Instructor tempInstructor);
    void update(Course tempCourse);
  
    Course findCourseById(int theId);
    void deleteCourseById(int theId);
    void save(Course theCourse);
  
    Course findCourseAndReviewsByCourseId(int theId);
    Course findCourseAndStudentsByCourseId(int theId);
    Student findStudentAndCoursesByStudentId(int theId);
  
    void update(Student tempStudent);
    void deleteStudentById(int theId);
}
```

```java
@Repository
public class AppDAOImpl implements AppDAO {

    private EntityManager entityManager;

    @Autowired
    public AppDAOImpl(EntityManager entityManager) {
        this.entityManager = entityManager;
    }

    @Override
    @Transactional
    public void save(Instructor theInstructor) {
        entityManager.persist(theInstructor);
    }

    @Override
    public Instructor findInstructorById(int theId) {
        return entityManager.find(Instructor.class, theId);
    }

    @Override
    @Transactional
    public void deleteInstructorById(int theId) {
        Instructor tempInstructor = entityManager.find(Instructor.class, theId);
        List<Course> courses = tempInstructor.getCourses();
        for (Course tempCourse : courses) {
            tempCourse.setInstructor(null);
        }
        entityManager.remove(tempInstructor);
    }

    @Override
    public InstructorDetail findInstructorDetailById(int theId) {
        return entityManager.find(InstructorDetail.class, theId);
    }

    @Override
    @Transactional
    public void deleteInstructorDetailById(int theId) {
        InstructorDetail tempInstructorDetail = entityManager.find(InstructorDetail.class, theId);
        tempInstructorDetail.getInstructor().setInstructorDetail(null);
        entityManager.remove(tempInstructorDetail);
    }

    @Override
    public List<Course> findCourseByInstructorId(int theId) {
        TypedQuery<Course> query = entityManager.createQuery(
          "from Course where instructor.id = :data", Course.class);
      
        query.setParameter("data", theId);
        List<Course> courses = query.getResultList();
        return courses;
    }

    @Override
    public Instructor findInstructorByIdJoinFetch(int theId) {
        TypedQuery<Instructor> query = entityManager.createQuery(
          "select i from Instructor i"
                + "JOIN FETCH i.courses "
                + "JOIN FETCH i.instructorDetail "
                + "where i.id = :data", Instructor.class);

        query.setParameter("data", theId);
        Instructor instructor = query.getSingleResult();
        return instructor;
    }

    @Override
    @Transactional
    public void update(Instructor tempInstructor) {
        entityManager.merge(tempInstructor);
    }

    @Override
    @Transactional
    public void update(Course tempCourse) {
        entityManager.merge(tempCourse);
    }

    @Override
    public Course findCourseById(int theId) {
        return entityManager.find(Course.class, theId);
    }

    @Override
    @Transactional
    public void deleteCourseById(int theId) {
        Course tempCourse = entityManager.find(Course.class, theId);
        entityManager.remove(tempCourse);
    }

    @Override
    @Transactional
    public void save(Course theCourse) {
        entityManager.persist(theCourse);
    }

    @Override
    public Course findCourseAndReviewsByCourseId(int theId) {
        TypedQuery<Course> query = entityManager.createQuery(
                "select c from Course c "
                        + "JOIN FETCH c.reviews "
                        + "where c.id = :data", Course.class);
      
        query.setParameter("data", theId);
        Course course = query.getSingleResult();
        return course;
    }

    @Override
    public Course findCourseAndStudentsByCourseId(int theId) {
        TypedQuery<Course> query = entityManager.createQuery(
                "select c from Course c "
                        + "JOIN FETCH c.students "
                        + "where c.id = :data", Course.class);
      
        query.setParameter("data", theId);
        Course course = query.getSingleResult();
        return course;
    }

    @Override
    public Student findStudentAndCoursesByStudentId(int theId) {
        TypedQuery<Student> query = entityManager.createQuery(
                "select s from Student s "
                        + "JOIN FETCH s.courses "
                        + "where s.id = :data", Student.class);

        query.setParameter("data", theId);
        Student student = query.getSingleResult();
        return student;
    }

    @Override
    @Transactional
    public void update(Student tempStudent) {
        entityManager.merge(tempStudent);
    }

    @Override
    @Transactional
    public void deleteStudentById(int theId) {
        Student tempStudent = entityManager.find(Student.class, theId);
        entityManager.remove(tempStudent);
    }
}
```



## Entity

```java
@Entity
@Table(name = "course")
public class Course {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "id")
    private int id;

    @Column(name = "title")
    private String title;

    @ManyToOne(cascade = {CascadeType.PERSIST, CascadeType.MERGE, 
                          CascadeType.DETACH, CascadeType.REFRESH})
    @JoinColumn(name = "instructor_id")
    private Instructor instructor;

    @OneToMany(fetch = FetchType.LAZY, cascade = CascadeType.ALL)
    @JoinColumn(name = "course_id")
    private List<Review> reviews;

    @ManyToMany(fetch = FetchType.LAZY, 
                cascade = {CascadeType.PERSIST, CascadeType.MERGE,
                           CascadeType.DETACH, CascadeType.REFRESH})
    @JoinTable(
            name = "course_student",
            joinColumns = @JoinColumn(name = "course_id"),
            inverseJoinColumns = @JoinColumn(name = "student_id"))
    private List<Student> students;

    public Course() {

    }

    public Course(String title) {
        this.title = title;
    }

    // getter and setter
  	// ... ...

    public void addReview(Review theReview) {
        if (reviews == null) {
            reviews = new ArrayList<>();
        }
        reviews.add(theReview);
    }

    public void addStudent(Student theStudent) {
        if (students == null) {
            students = new ArrayList<>();
        }
        students.add(theStudent);
    }

    // @Override toString()
}
```

```java
@Entity
@Table(name = "instructor")
public class Instructor {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "id")
    private int id;

    @Column(name = "first_name")
    private String firstName;

    @Column(name = "last_name")
    private String lastName;

    @Column(name = "email")
    private String email;

    @OneToOne(cascade = CascadeType.ALL)
    @JoinColumn(name = "instructor_detail_id")
    private InstructorDetail instructorDetail;

    @OneToMany(mappedBy = "instructor",
            fetch = FetchType.LAZY,
            cascade = {CascadeType.PERSIST, CascadeType.MERGE, 
                       CascadeType.DETACH, CascadeType.REFRESH})
    private List<Course> courses;

    public Instructor() {

    }

    public Instructor(String firstName, String lastName, String email) {
        this.firstName = firstName;
        this.lastName = lastName;
        this.email = email;
    }

    // getter and setter
  	// ... ...

    public void add(Course tempCourse) {
        if (courses == null) {
            courses = new ArrayList<>();
        }
        courses.add(tempCourse);
        tempCourse.setInstructor(this);
    }

    // @Override toString()
}
```

```java
@Entity
@Table(name="instructor_detail")
public class InstructorDetail {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name="id")
    private int id;

    @Column(name="youtube_channel")
    private String youtubeChannel;

    @Column(name="hobby")
    private String hobby;

    @OneToOne(mappedBy = "instructorDetail", 
              cascade = {CascadeType.DETACH,CascadeType.MERGE,
         								 CascadeType.PERSIST,CascadeType.REFRESH})
    private Instructor instructor;

    public InstructorDetail() {

    }

    public InstructorDetail(String youtubeChannel, String hobby) {
        this.youtubeChannel = youtubeChannel;
        this.hobby = hobby;
    }

    // getter and setter
  	// ... ...

    // @Override toString()
}
```

```java
@Entity
@Table(name="review")
public class Review {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name="id")
    private int id;

    @Column(name="comment")
    private String comment;

    public Review() {

    }

    public Review(String comment) {
        this.comment = comment;
    }

    // getter and setter
  	// ... ...

    // @Override toString()
}
```

```java
@Entity
@Table(name = "student")
public class Student {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "id")
    private int id;

    @Column(name = "first_name")
    private String firstName;

    @Column(name = "last_name")
    private String lastName;

    @Column(name = "email")
    private String email;

    @ManyToMany(fetch = FetchType.LAZY,
            		cascade = {CascadeType.PERSIST, CascadeType.MERGE, 
                       		 CascadeType.DETACH, CascadeType.REFRESH})
    @JoinTable(
            name = "course_student",
            joinColumns = @JoinColumn(name = "student_id"),
            inverseJoinColumns = @JoinColumn(name = "course_id"))
    private List<Course> courses;

    public Student() {

    }

    public Student(String firstName, String lastName, String email) {
        this.firstName = firstName;
        this.lastName = lastName;
        this.email = email;
    }
  
  	// getter and setter
  	// ... ...

    public void addCourse(Course theCourse) {
        if (courses == null) {
            courses = new ArrayList<>();
        }
        courses.add(theCourse);
    }
  
    // @Override toString()
}
```



## Application

```java
@SpringBootApplication
public class JpaOneToOneUniApplication {
	@Bean
	public CommandLineRunner commandLineRunner(AppDAO appDAO) {
		return runner->{
			// createInstructor(appDAO);
			// findInstructor(appDAO);
			// deleteInstructor(appDAO);
			// findInstructorDetail(appDAO);
			// deleteInstructorDetail(appDAO);

			// createInstructorWithCourses(appDAO);
			// findInstructorWithCourse(appDAO);
			// findCoursesForInstructor(appDAO);
			// findInstructorWithCourseJoinFetch(appDAO);
			// updateInstructor(appDAO);
			// updateCourse(appDAO);
			// deleteInstructor(appDAO);
			// deleteCourse(appDAO);

			// createCourseAndReviews(appDAO);
			// retrieveCourseAndReview(appDAO);
			// deleteCourseAndReviews(appDAO);

			// createCourseAndStudents(appDAO);
			// findCoursesAndStudents(appDAO);
			// findStudentAndCourses(appDAO);
			// addMoreCoursesForStudent(appDAO);
			// deleteCourse(appDAO);
			deleteStudent(appDAO);
		};
	}

	private void deleteStudent(AppDAO appDAO) {
		int theId = 1;
		appDAO.deleteStudentById(theId);
	}

	private void addMoreCoursesForStudent(AppDAO appDAO) {
		int theId = 2;
		Student tempStudent = appDAO.findStudentAndCoursesByStudentId(theId);

		Course tempCourse1 = new Course("Rubik's Cube - How to Speed Cube");
		Course tempCourse2 = new Course("Atari 2600 - Game Development");

		tempStudent.addCourse(tempCourse1);
		tempStudent.addCourse(tempCourse2);

		appDAO.update(tempStudent);
	}

	private void findStudentAndCourses(AppDAO appDAO) {
		int theId = 2;
		Student tempStudent = appDAO.findStudentAndCoursesByStudentId(theId);
	}

	private void findCoursesAndStudents(AppDAO appDAO) {
		int theId = 10;
		Course tempCourse = appDAO.findCourseAndStudentsByCourseId(theId
	}

	private void createCourseAndStudents(AppDAO appDAO) {
		Course tempCourse = new Course("Pacman - Now To Score One Million Points");

		Student tempStudent1 = new Student("John", "Doe", "john@gmail.com");
		Student tempStudent2 = new Student("Mary", "Public", "mary@gmail.com");

		tempCourse.addStudent(tempStudent1);
		tempCourse.addStudent(tempStudent2);

		appDAO.save(tempCourse);
	}

	private void deleteCourseAndReviews(AppDAO appDAO) {
		int theId = 10;
		appDAO.deleteCourseById(theId);
	}

	private void retrieveCourseAndReview(AppDAO appDAO) {
		int theId = 10;
		Course tempCourse = appDAO.findCourseAndReviewsByCourseId(theId);
	}

	private void createCourseAndReviews(AppDAO appDAO) {
		Course tempCourse = new Course("Pacman - How To Score On Million Points");
		tempCourse.addReview(new Review("Great course ... love it!"));
		tempCourse.addReview(new Review("Cool course, job well done."));
		tempCourse.addReview(new Review("What a dumb course, you are in idiot!"));
		appDAO.save(tempCourse);
	}


	private void deleteCourse(AppDAO appDAO) {
		int theId = 10;
		appDAO.deleteCourseById(theId);
	}

	private void updateCourse(AppDAO appDAO) {
		int theId = 10;
		Course tempCourse = appDAO.findCourseById(theId);
		tempCourse.setTitle("Enjoy the Simple Things");
    
		appDAO.update(tempCourse);
	}

	private void updateInstructor(AppDAO appDAO){
		int theId = 1;
		Instructor tempInstructor = appDAO.findInstructorById(theId);
		tempInstructor.setLastName("TESTER");

		appDAO.update(tempInstructor);
	}

	private void findInstructorWithCourseJoinFetch(AppDAO appDAO) {
		int theId = 1;
		Instructor tempInstructor = appDAO.findInstructorByIdJoinFetch(theId);
	}

	private void findCoursesForInstructor(AppDAO appDAO) {
		int theId = 1;
		Instructor tempInstructor = appDAO.findInstructorById(theId);

		List<Course> courses = appDAO.findCourseByInstructorId(theId);
		tempInstructor.setCourses(courses);
	}

	private void findInstructorWithCourse(AppDAO appDAO) {
		int theId = 1;
		Instructor tempInstructor = appDAO.findInstructorById(theId);
	}

	private void createInstructorWithCourses(AppDAO appDAO) {
		// new Instructor
		Instructor tempInstructor = new Instructor("Susan", "Public", "public@gmail.com");
		// new InstructorDetail
		InstructorDetail tempInstructorDetail = 
      new InstructorDetail("http://www.youtube/public", "code");

		// associate the objects
		tempInstructor.setInstructorDetail(tempInstructorDetail);

		// create courses
		Course tempCourse1 = new Course("Air Guitar");
		Course tempCourse2 = new Course("The Pinball Masterclass");

		tempInstructor.add(tempCourse1);
		tempInstructor.add(tempCourse2);
    
		appDAO.save(tempInstructor);
	}

	private void deleteInstructorDetail(AppDAO appDAO) {
		int theId = 2;
		appDAO.deleteInstructorDetailById(theId);
	}

	private void findInstructorDetail(AppDAO appDAO) {
		int theId = 2;
		InstructorDetail tempInstructorDetail = appDAO.findInstructorDetailById(theId);
	}

	private void deleteInstructor(AppDAO appDAO) {
		int theId = 1;
		appDAO.deleteInstructorById(theId);
	}

	private void findInstructor(AppDAO appDAO) {
		int theId = 1;
		Instructor tempInstructor = appDAO.findInstructorById(theId);
	}

	private void createInstructor(AppDAO appDAO) {
		// new Instructor
		Instructor tempInstructor = new Instructor("Chad", "Darby", "darby@gmail.com");
		// new InstructorDetail
		InstructorDetail tempInstructorDetail = 
      new InstructorDetail("http://www.youtube/darby", "code");

		// associate the objects
		tempInstructor.setInstructorDetail(tempInstructorDetail);
		appDAO.save(tempInstructor);
	}
}
```