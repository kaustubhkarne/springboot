## VIT Student Result System

## Stack: React (Vite) + Spring Boot + MySQL


# 1️⃣ What this project does & what we used

# Goal
A web app to manage one semester result of VIT students with:

- Student details
- Fixed courses (subjects)
- Marks: MSE (30%), ESE (70%)
- Computed total and grade

# Tech used

**Frontend**
- React (created using Vite)
- Axios (for calling backend APIs)
- Tailwind CSS (for styling)
- lucide-react icons

**Backend**
- Spring Boot (Java)
- Spring Web + Spring Data JPA
- MySQL Driver

**Database**
- MySQL DB (e.g. vit_results)

# Final database design
We changed things to a cleaner, normalized structure:

| Table | Fields |
Student -  studentId (PK), name 
Course -  courseId (PK), title 
Result -  id (PK), mse, ese, total, grade, cgpa, semester, student_id (FK), course_id (FK) 


### 2️⃣ File structure & what files do

#### 🖥 Backend (Spring Boot project – e.g. `resultsystem/`)

**1. Entry point**
`src/main/java/com/vit/resultsystem/ResultSystemApplication.java`  
→ Main Spring Boot class. Runs the backend on http://localhost:8080.

**2. Models (Entities)**  
Under: `src/main/java/com/vit/resultsystem/model/`

- `Student.java` — Student entity with studentId + name + list of results
- `Course.java` — Course entity with courseId + title + list of results
- `Result.java` — Result entity (marks, grade, semester) + ManyToOne relation to Student & Course

**3. Repositories**  
Under: `src/main/java/com/vit/resultsystem/repository/`

- StudentRepository → `JpaRepository<Student, String>`
- CourseRepository → `JpaRepository<Course, String>`
- ResultRepository → `JpaRepository<Result, Long>` + `findByStudent()`, `findByStudentAndCourse()`

**4. Controllers**  
Under: `src/main/java/com/vit/resultsystem/controller/`

- `StudentController.java` — GET `/api/students`
- `CourseController.java` — GET `/api/courses`
- `ResultController.java` — POST `/api/results`, GET `/api/results/student/{studentId}`

**5. CORS Config**
Allows React on `5173` to call Spring Boot `8080`.

**6. Database config**
`src/main/resources/application.properties` contains datasource & JPA configs.

---

### 🌐 Frontend (Vite React project – e.g. `vit-result-system/`)

Key files:
- `vite.config.js`, `package.json`, `src/main.jsx`, `src/App.jsx`

Main UI in:
```
src/VITResultSystem.jsx
```

Features inside:
- Fetch students & courses using useEffect
- Add result form (POST `/api/results`)
- Dashboard
- Student Results tab
- Analytics tab (average marks & grade distribution)

---

### 🖥 How to run the Backend (Spring Boot)

1. Start MySQL.
2. Create database:
   ```
   CREATE DATABASE vit_results;
   ```
3. Open the Spring Boot project in IntelliJ / Eclipse.
4. Check `application.properties` for correct DB username & password.
5. Run the backend by launching the main Java file:
   
   ResultSystemApplication.java

The backend will start at:
👉 http://localhost:8080


#### 🌐 Frontend (React)
```
npm install
npm run dev
```
Open browser: **http://localhost:5173**

⚠️ Backend must be running when adding results.
