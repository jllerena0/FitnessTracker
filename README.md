# FitnessTracker

-- ===============================
-- User Table
-- ===============================
CREATE TABLE User (
    user_id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    date_of_birth DATE,
    gender VARCHAR(20),
    age INT,
    activity_level VARCHAR(50),
    email VARCHAR(100) UNIQUE,
    experience VARCHAR(50),
    subscription_status VARCHAR(20)
);

-- ===============================
-- Goal Table
-- ===============================
CREATE TABLE Goal (
    goal_id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,
    goal_type VARCHAR(50),
    goal_name VARCHAR(100),
    target_value DECIMAL(10,2),
    starting_value DECIMAL(10,2),
    current_value DECIMAL(10,2),
    unit_of_measure VARCHAR(20),
    start_date DATE,
    target_date DATE,
    status VARCHAR(20),
    frequency VARCHAR(20),
    notes TEXT,
    related_workout_types VARCHAR(100),
    priority_level VARCHAR(20),
    FOREIGN KEY (user_id) REFERENCES User(user_id)
        ON DELETE CASCADE
        ON UPDATE CASCADE
);

-- ===============================
-- Workout Table
-- ===============================
CREATE TABLE Workout (
    workout_id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,
    workout_plan_id INT,
    template_id INT,
    exercise VARCHAR(100),
    workout_name VARCHAR(100),
    scheduled_datetime DATETIME,
    active_exercise_time INT, -- in minutes
    total_distance DECIMAL(10,2),
    workout_type VARCHAR(50),
    total_calories_burned INT,
    difficulty VARCHAR(20),
    muscle_groups VARCHAR(100),
    description TEXT,
    instruction TEXT,
    equipment VARCHAR(100),
    category VARCHAR(50),
    media VARCHAR(255),
    duration INT, -- in minutes
    FOREIGN KEY (user_id) REFERENCES User(user_id)
        ON DELETE CASCADE
        ON UPDATE CASCADE
);

-- ===============================
-- Body Metric Table
-- ===============================
CREATE TABLE BodyMetric (
    metric_id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,
    weight DECIMAL(5,2),
    height DECIMAL(5,2),
    body_fat_percentage DECIMAL(5,2),
    heart_rate INT,
    vo2_max DECIMAL(5,2),
    sleep_hours DECIMAL(4,2),
    other_metrics TEXT,
    measurement_date DATE NOT NULL,
    FOREIGN KEY (user_id) REFERENCES User(user_id)
        ON DELETE CASCADE
        ON UPDATE CASCADE
);

-- ===============================
-- Nutrition Table
-- ===============================
CREATE TABLE Nutrition (
    nutrition_id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,
    calories INT,
    protein DECIMAL(5,2),
    carbs DECIMAL(5,2),
    fat DECIMAL(5,2),
    water DECIMAL(5,2),
    diet_consistency VARCHAR(50),
    log_date DATE NOT NULL,
    FOREIGN KEY (user_id) REFERENCES User(user_id)
        ON DELETE CASCADE
        ON UPDATE CASCADE
);
