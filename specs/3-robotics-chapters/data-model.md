# Data Model: Robotics Chapters

**Feature**: Chapters 3-6 - Physical AI & Humanoid Robotics Textbook
**Date**: 2025-12-07

## Core Entities

### Lesson
Represents a single learning unit within the robotics chapters.

**Fields:**
- `id`: String - Unique identifier following format "X.Y-topic-description" (e.g., "3.1-ros-2-architecture-overview")
- `title`: String - Human-readable title of the lesson
- `sidebar_label`: String - Short label for navigation sidebar
- `chapter`: Integer - Chapter number (3, 4, 5, or 6)
- `lesson_number`: Float - Lesson number within chapter
- `priority`: Enum (P1, P2) - Development priority level
- `learning_objectives`: Array of String - List of 3-5 learning objectives
- `content_structure`: Object - Contains the lesson sections
- `word_count`: Integer - Estimated word count (target: 300-700)
- `created_date`: Date - Date the lesson was created
- `last_updated`: Date - Date of last modification

**Validation Rules:**
- `id` must follow the pattern: `^[0-9]+\\.[0-9]+-[a-z0-9-]+$`
- `title` must be 10-100 characters
- `learning_objectives` must contain 3-5 items
- `priority` must be one of P1, P2
- `word_count` must be between 300 and 700
- `chapter` must be 3, 4, 5, or 6

### Content Structure
Defines the organization of content within a lesson.

**Fields:**
- `introduction`: String - Opening section that sets context
- `main_theory`: String - Core explanation of concepts
- `diagrams`: Array of Object - Visual representations and ASCII diagrams
- `examples`: Array of String - Practical examples and applications
- `practical_notes`: Array of String - Implementation considerations
- `hands_on_exercise`: String - Mini exercise or hands-on activity
- `summary`: String - Brief recap of key points
- `glossary`: Object - Terms and definitions
- `quiz`: Array of Object - MCQ questions and answers

**Validation Rules:**
- `introduction` must be 50-150 words
- `main_theory` must be 150-400 words
- `examples` must include at least 1 practical example
- `quiz` must contain 3-5 questions
- Total content must be 300-700 words

### Chapter
Represents a collection of related lessons on a specific topic.

**Fields:**
- `chapter_number`: Integer - The chapter number (3, 4, 5, or 6)
- `title`: String - Title of the chapter
- `topic`: String - Main topic area (e.g., "ROS 2 Fundamentals", "Robot Modeling & Simulation")
- `lessons`: Array of Object - List of lessons in this chapter
- `total_lessons`: Integer - Number of lessons in the chapter
- `prerequisites`: Array of String - Knowledge required before this chapter

**Validation Rules:**
- `chapter_number` must be between 3 and 6
- `total_lessons` must match the actual number of lessons
- `topic` must be one of the specified chapter topics

### Learning Objective
Represents a specific educational goal for a lesson.

**Fields:**
- `text`: String - The objective statement
- `difficulty`: Enum (Beginner, Intermediate) - Complexity level
- `type`: Enum (Knowledge, Comprehension, Application) - Cognitive level
- `related_subtopics`: Array of String - Subtopics that support this objective

**Validation Rules:**
- `text` must be 10-50 characters
- `difficulty` must be Beginner or Intermediate
- `type` must be Knowledge, Comprehension, or Application

### Subtopic
Represents a focused concept or technique covered within a lesson.

**Fields:**
- `title`: String - Title of the subtopic
- `content`: String - Explanation of the subtopic
- `example`: String - Practical example of the subtopic
- `diagram_reference`: String - Reference to associated diagram or ASCII art
- `difficulty`: Enum (Beginner, Intermediate) - Complexity level

**Validation Rules:**
- `title` must be 5-30 characters
- `content` must be 40-100 words
- `difficulty` must be Beginner or Intermediate
- Each lesson must have 4-7 subtopics

### Quiz Question
Represents a multiple-choice question for lesson assessment.

**Fields:**
- `question`: String - The question text
- `options`: Array of Object - Possible answer choices (exactly 4)
- `correct_answer`: String - The letter identifier of correct option (A, B, C, or D)
- `explanation`: String - Explanation of why the answer is correct
- `difficulty`: Enum (Beginner, Intermediate) - Difficulty level

**Validation Rules:**
- `options` must contain exactly 4 choices
- `correct_answer` must match one of the option identifiers (A, B, C, or D)
- `difficulty` must be Beginner or Intermediate

## Relationships

### Chapter → Lesson
- One chapter contains multiple lessons
- Each lesson belongs to exactly one chapter

### Lesson → Learning Objective
- One lesson has multiple learning objectives (3-5)
- Each learning objective belongs to exactly one lesson

### Lesson → Subtopic
- One lesson covers multiple subtopics (4-7)
- Each subtopic belongs to exactly one lesson

### Lesson → Quiz Question
- One lesson contains multiple quiz questions (3-5)
- Each quiz question belongs to exactly one lesson

## State Transitions

### Lesson States
- `Draft`: Initial state when lesson structure is planned
- `Content_In_Progress`: When content is being written
- `Review_Pending`: When content is complete and ready for review
- `Completed`: When lesson is finalized and approved

**Transitions:**
- `Draft` → `Content_In_Progress`: When writing begins
- `Content_In_Progress` → `Review_Pending`: When content is complete
- `Review_Pending` → `Content_In_Progress`: When changes are requested
- `Review_Pending` → `Completed`: When approved