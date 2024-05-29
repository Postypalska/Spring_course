# Spring_course
### Функціональні Вимоги

1. **Управління Студентами:**
   - Створення, читання, оновлення та видалення записів студентів.
   - Отримання списку всіх студентів.

2. **Управління Гуртожитками:**
   - Створення, читання, оновлення та видалення записів гуртожитків.
   - Отримання списку всіх гуртожитків.

3. **Управління Кімнатами:**
   - Створення, читання, оновлення та видалення записів кімнат.
   - Отримання списку всіх кімнат.
   - Отримання кімнат по гуртожитку.

4. **Управління Резерваціями:**
   - Створення, читання, оновлення та видалення записів резервацій.
   - Отримання списку всіх резервацій.
   - Отримання резервацій по студенту та кімнаті.
   - Перевірка наявності місць у кімнаті перед створенням резервації.

### Макети

#### 1. Управління Студентами
**Сторінка Списку Студентів**
- Таблиця з переліком всіх студентів: ID, Ім'я, Прізвище, Курс, Група.
- Кнопки: Додати Студента, Редагувати, Видалити поруч з кожним студентом.

**Сторінка Додавання/Редагування Студента**
- Поля форми: Ім'я, Прізвище, Курс, Група.
- Кнопки: Зберегти, Скасувати.

#### 2. Управління Гуртожитками
**Сторінка Списку Гуртожитків**
- Таблиця з переліком всіх гуртожитків: ID, Назва, Адреса, Кількість Кімнат.
- Кнопки: Додати Гуртожиток, Редагувати, Видалити поруч з кожним гуртожитком.

**Сторінка Додавання/Редагування Гуртожитку**
- Поля форми: Назва, Адреса, Кількість Кімнат.
- Кнопки: Зберегти, Скасувати.

#### 3. Управління Кімнатами
**Сторінка Списку Кімнат**
- Таблиця з переліком всіх кімнат: ID, Номер Кімнати, Гуртожиток, Стать, Вмістимість.
- Випадаючий список для фільтрації по гуртожитку.
- Кнопки: Додати Кімнату, Редагувати, Видалити поруч з кожною кімнатою.

**Сторінка Додавання/Редагування Кімнати**
- Поля форми: Номер Кімнати, Гуртожиток, Стать, Вмістимість.
- Кнопки: Зберегти, Скасувати.

#### 4. Управління Резерваціями
**Сторінка Списку Резервацій**
- Таблиця з переліком всіх резервацій: ID, Студент, Кімната, Дата Початку, Дата Закінчення.
- Кнопки: Додати Резервацію, Редагувати, Видалити поруч з кожною резервацією.

**Сторінка Додавання/Редагування Резервації**
- Поля форми: Студент (випадаючий список), Кімната (випадаючий список), Дата Початку, Дата Закінчення.
- Кнопки: Зберегти, Скасувати.

### Поведінка Системи

- **CRUD Операції:** Кожна сутність (Студент, Гуртожиток, Кімната, Резервація) підтримує операції створення, читання, оновлення та видалення.
- **Валідація:** Забезпечити, щоб вмістимість кімнати не перевищувалася при створенні резервацій.
- **Фільтрація:** Кімнати можуть фільтруватися по гуртожитку.
- **Консистентність:** Забезпечити реферальну цілісність при видаленні записів (наприклад, при видаленні гуртожитку правильно обробляти пов’язані кімнати та резервації).

### REST API Ендпойнти

#### Ендпойнти для Студентів
- **GET /api/students:** Отримати всіх студентів.
- **GET /api/students/{id}:** Отримати студента за ID.
- **POST /api/students:** Створити нового студента.
- **PUT /api/students/{id}:** Оновити студента за ID.
- **DELETE /api/students/{id}:** Видалити студента за ID.

#### Ендпойнти для Гуртожитків
- **GET /api/dormitories:** Отримати всі гуртожитки.
- **GET /api/dormitories/{id}:** Отримати гуртожиток за ID.
- **POST /api/dormitories:** Створити новий гуртожиток.
- **PUT /api/dormitories/{id}:** Оновити гуртожиток за ID.
- **DELETE /api/dormitories/{id}:** Видалити гуртожиток за ID.

#### Ендпойнти для Кімнат
- **GET /api/rooms:** Отримати всі кімнати.
- **GET /api/rooms/{id}:** Отримати кімнату за ID.
- **GET /api/dormitories/{dormitoryId}/rooms:** Отримати всі кімнати за ID гуртожитку.
- **POST /api/rooms:** Створити нову кімнату.
- **PUT /api/rooms/{id}:** Оновити кімнату за ID.
- **DELETE /api/rooms/{id}:** Видалити кімнату за ID.

#### Ендпойнти для Резервацій
- **GET /api/reservations:** Отримати всі резервації.
- **GET /api/reservations/{id}:** Отримати резервацію за ID.
- **GET /api/students/{studentId}/reservations:** Отримати всі резервації за ID студента.
- **GET /api/rooms/{roomId}/reservations:** Отримати всі резервації за ID кімнати.
- **POST /api/reservations:** Створити нову резервацію.
- **PUT /api/reservations/{id}:** Оновити резервацію за ID.
- **DELETE /api/reservations/{id}:** Видалити резервацію за ID.

### Реалізація

1. **Налаштування Проекту:**
   - Ініціалізуйте проект Spring Boot з залежностями: Web, JPA, H2 Database, DevTools.

2. **Класи Сутностей:**
   Визначте класи сутностей відповідно до діаграми.

#### Student.java
```java
@Entity
public class Student {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long studentId;
    private String name;
    private String surname;
    private String course;
    private String group;

    // Геттери та Сеттери
}
```

#### Dormitory.java
```java
@Entity
public class Dormitory {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long dormitoryId;
    private String name;
    private String address;
    private int numberOfRooms;

    // Геттери та Сеттери
}
```

#### Room.java
```java
@Entity
public class Room {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long roomId;
    private String roomNum;
    @ManyToOne
    @JoinColumn(name = "dormitory_id")
    private Dormitory dormitory;
    private String gender;
    private int capacity;

    // Геттери та Сеттери
}
```

#### Reservation.java
```java
@Entity
public class Reservation {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long reservationId;
    private LocalDate startDate;
    private LocalDate endDate;
    @ManyToOne
    @JoinColumn(name = "student_id")
    private Student student;
    @ManyToOne
    @JoinColumn(name = "room_id")
    private Room room;

    // Геттери та Сеттери
}
```

3. **Інтерфейси Репозиторіїв:**

#### StudentRepository.java
```java
public interface StudentRepository extends JpaRepository<Student, Long> {
}
```

#### DormitoryRepository.java
```java
public interface DormitoryRepository extends JpaRepository<Dormitory, Long> {
}
```

#### RoomRepository.java
```java
public interface RoomRepository extends JpaRepository<Room, Long> {
    List<Room>

 findByDormitory(Dormitory dormitory);
}
```

#### ReservationRepository.java
```java
public interface ReservationRepository extends JpaRepository<Reservation, Long> {
    List<Reservation> findByStudent(Student student);
    List<Reservation> findByRoom(Room room);
}
```

4. **Сервісний Шар:**

#### StudentService.java
```java
@Service
public class StudentService {
    @Autowired
    private StudentRepository studentRepository;

    public List<Student> getAllStudents() {
        return studentRepository.findAll();
    }

    public Student getStudentById(Long id) {
        return studentRepository.findById(id).orElseThrow(() -> new ResourceNotFoundException("Студента не знайдено"));
    }

    public Student createStudent(Student student) {
        return studentRepository.save(student);
    }

    public Student updateStudent(Long id, Student studentDetails) {
        Student student = getStudentById(id);
        student.setName(studentDetails.getName());
        student.setSurname(studentDetails.getSurname());
        student.setCourse(studentDetails.getCourse());
        student.setGroup(studentDetails.getGroup());
        return studentRepository.save(student);
    }

    public void deleteStudent(Long id) {
        Student student = getStudentById(id);
        studentRepository.delete(student);
    }
}
```

#### DormitoryService.java
```java
@Service
public class DormitoryService {
    @Autowired
    private DormitoryRepository dormitoryRepository;

    public List<Dormitory> getAllDormitories() {
        return dormitoryRepository.findAll();
    }

    public Dormitory getDormitoryById(Long id) {
        return dormitoryRepository.findById(id).orElseThrow(() -> new ResourceNotFoundException("Гуртожиток не знайдено"));
    }

    public Dormitory createDormitory(Dormitory dormitory) {
        return dormitoryRepository.save(dormitory);
    }

    public Dormitory updateDormitory(Long id, Dormitory dormitoryDetails) {
        Dormitory dormitory = getDormitoryById(id);
        dormitory.setName(dormitoryDetails.getName());
        dormitory.setAddress(dormitoryDetails.getAddress());
        dormitory.setNumberOfRooms(dormitoryDetails.getNumberOfRooms());
        return dormitoryRepository.save(dormitory);
    }

    public void deleteDormitory(Long id) {
        Dormitory dormitory = getDormitoryById(id);
        dormitoryRepository.delete(dormitory);
    }
}
```

#### RoomService.java
```java
@Service
public class RoomService {
    @Autowired
    private RoomRepository roomRepository;

    public List<Room> getAllRooms() {
        return roomRepository.findAll();
    }

    public Room getRoomById(Long id) {
        return roomRepository.findById(id).orElseThrow(() -> new ResourceNotFoundException("Кімнату не знайдено"));
    }

    public List<Room> getRoomsByDormitory(Long dormitoryId) {
        Dormitory dormitory = dormitoryRepository.findById(dormitoryId).orElseThrow(() -> new ResourceNotFoundException("Гуртожиток не знайдено"));
        return roomRepository.findByDormitory(dormitory);
    }

    public Room createRoom(Room room) {
        return roomRepository.save(room);
    }

    public Room updateRoom(Long id, Room roomDetails) {
        Room room = getRoomById(id);
        room.setRoomNum(roomDetails.getRoomNum());
        room.setDormitory(roomDetails.getDormitory());
        room.setGender(roomDetails.getGender());
        room.setCapacity(roomDetails.getCapacity());
        return roomRepository.save(room);
    }

    public void deleteRoom(Long id) {
        Room room = getRoomById(id);
        roomRepository.delete(room);
    }
}
```

#### ReservationService.java
```java
@Service
public class ReservationService {
    @Autowired
    private ReservationRepository reservationRepository;

    public List<Reservation> getAllReservations() {
        return reservationRepository.findAll();
    }

    public Reservation getReservationById(Long id) {
        return reservationRepository.findById(id).orElseThrow(() -> new ResourceNotFoundException("Резервацію не знайдено"));
    }

    public List<Reservation> getReservationsByStudent(Long studentId) {
        Student student = studentRepository.findById(studentId).orElseThrow(() -> new ResourceNotFoundException("Студента не знайдено"));
        return reservationRepository.findByStudent(student);
    }

    public List<Reservation> getReservationsByRoom(Long roomId) {
        Room room = roomRepository.findById(roomId).orElseThrow(() -> new ResourceNotFoundException("Кімнату не знайдено"));
        return reservationRepository.findByRoom(room);
    }

    public Reservation createReservation(Reservation reservation) {
        // Перевірка наявності місць у кімнаті
        Room room = reservation.getRoom();
        List<Reservation> existingReservations = reservationRepository.findByRoom(room);
        if (existingReservations.size() >= room.getCapacity()) {
            throw new RoomCapacityExceededException("Вмістимість кімнати перевищено");
        }
        return reservationRepository.save(reservation);
    }

    public Reservation updateReservation(Long id, Reservation reservationDetails) {
        Reservation reservation = getReservationById(id);
        reservation.setStartDate(reservationDetails.getStartDate());
        reservation.setEndDate(reservationDetails.getEndDate());
        reservation.setStudent(reservationDetails.getStudent());
        reservation.setRoom(reservationDetails.getRoom());
        return reservationRepository.save(reservation);
    }

    public void deleteReservation(Long id) {
        Reservation reservation = getReservationById(id);
        reservationRepository.delete(reservation);
    }
}
```
