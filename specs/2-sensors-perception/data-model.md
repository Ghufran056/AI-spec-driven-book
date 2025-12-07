# Data Model: Sensors & Perception

**Feature**: Chapter 2 - Sensors & Perception
**Date**: 2025-12-07

## Core Entities

### Lesson
Represents a single learning unit within the Sensors & Perception chapter.

**Fields:**
- `id`: String - Unique identifier following format "X.Y-topic-description" (e.g., "2.1-introduction-to-robot-sensors")
- `title`: String - Human-readable title of the lesson
- `sidebar_label`: String - Short label for navigation sidebar
- `priority`: Enum (P1, P2, P3) - Development priority level
- `learning_objectives`: Array of String - List of 3-4 learning objectives
- `content_structure`: Object - Contains the lesson sections
- `created_date`: Date - Date the lesson was created
- `last_updated`: Date - Date of last modification

**Validation Rules:**
- `id` must follow the pattern: `^[0-9]+\\.[0-9]+-[a-z0-9-]+$`
- `title` must be 10-100 characters
- `learning_objectives` must contain 3-4 items
- `priority` must be one of P1, P2, or P3

### Content Structure
Defines the organization of content within a lesson.

**Fields:**
- `introduction`: String - Opening section that sets context
- `theory`: String - Main explanation of concepts
- `examples`: Array of String - Practical examples and applications
- `diagrams`: Array of Object - Visual representations
- `summary`: String - Brief recap of key points
- `glossary`: Object - Terms and definitions
- `quiz`: Array of Object - MCQ questions and answers

**Validation Rules:**
- `introduction` must be 100-500 words
- `theory` must contain 4-6 subtopics as specified
- `examples` must include at least 1 practical example
- `quiz` must contain 3-5 questions

### Sensor Type
Represents different categories of sensors used in robotics.

**Fields:**
- `name`: String - Technical name of the sensor type
- `description`: String - Brief explanation of what the sensor does
- `principle`: String - How the sensor works (physics/technology)
- `applications`: Array of String - Common use cases in robotics
- `advantages`: Array of String - Benefits of this sensor type
- `limitations`: Array of String - Constraints and drawbacks
- `typical_specifications`: Object - Common technical specifications

**Validation Rules:**
- `name` must be unique within the chapter
- `description` must be 50-200 characters
- `applications` must contain at least 2 use cases

### Perception Technique
Represents methods and algorithms used to interpret sensor data.

**Fields:**
- `name`: String - Name of the perception technique
- `description`: String - Explanation of the technique
- `principle`: String - How the technique works conceptually
- `applications`: Array of String - Use cases in robotics
- `complexity_level`: Enum (Basic, Intermediate, Advanced)
- `prerequisites`: Array of String - Knowledge required to understand
- `examples`: Array of String - Practical examples

**Validation Rules:**
- `complexity_level` must be Basic, Intermediate, or Advanced
- `prerequisites` must reference other lessons or concepts

### Quiz Question
Represents a multiple-choice question for lesson assessment.

**Fields:**
- `question`: String - The question text
- `options`: Array of Object - Possible answer choices
- `correct_answer`: String - The letter identifier of correct option
- `explanation`: String - Explanation of why the answer is correct
- `difficulty`: Enum (Easy, Medium, Hard)

**Validation Rules:**
- `options` must contain exactly 4 choices
- `correct_answer` must match one of the option identifiers
- `difficulty` must be Easy, Medium, or Hard

## Relationships

### Lesson → Sensor Type
- One lesson may cover one or more sensor types
- Each sensor type may be covered in multiple lessons (with different focus)

### Lesson → Perception Technique
- One lesson may introduce one or more perception techniques
- Each perception technique is typically covered in one lesson

### Lesson → Quiz Question
- One lesson contains multiple quiz questions
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