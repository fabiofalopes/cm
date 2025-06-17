**Objective:**

Analyze the provided course materials for "Computação Móvel" to create a single, consolidated study guide. This guide should distill the professor's core focus, recurring themes, and the most critical knowledge required to succeed in the final theoretical exam.

**Core Constraints:**

1.  **Final Output:** A single Markdown file named `guia_estudo_exame.md`.
2.  **Exam Sheet Rules:** The content must be optimized for being handwritten onto a single A4 sheet (front and back). This means it must be concise, dense, and **must not contain any code snippets (e.g., Dart, JSON)**. Text and simple conceptual diagrams are allowed.

**Source Materials to Analyze:**

*   `aulas-md/`: The detailed lecture notes.
*   `aulas-resumos/`: Your existing summaries, especially `13-resumo-final-exame.md`, which provides the exam structure.
*   `quiz/`: Quizzes and their solutions, which indicate likely question formats.
*   `youtube_transcripts/md/`: Transcripts of the professor's practical videos, which are key to understanding their emphasis and practical application of concepts.

**Execution Plan:**

1.  **Synthesize Professor's Focus:** Analyze all materials simultaneously to identify overlapping concepts. A topic that appears in the lectures, quizzes, and video transcripts is of the highest importance. The goal is to understand the professor's "philosophy" of mobile development.

2.  **Structure the Guide by Exam Topics:** Use the `13-resumo-final-exame.md` as the backbone for the new study guide. The structure should directly map to the exam parts:
    *   **Part 1: JSON Format (2 points):** Don't just show an example. Explain the *rules and logic* of mapping XML structures (nested tags, sibling tags, attributes) to their JSON equivalents (objects, arrays, key-value pairs).
    *   **Part 2: Callback Programming (2 points):** Explain the *conceptual flow* of callback-driven code. Focus on how state changes sequentially across different objects and scopes. Use the example from the summary to describe the step-by-step logic without writing the code itself.
    *   **Part 3: Flutter Concepts (4 points):** Provide clear, concise definitions for the core topics (Stateless vs. Stateful, Dependency Injection, `async`/`await`, Widget vs. Integration tests). For each, answer: What is it? Why is it important? When do you use it?
    *   **Part 4: Mobile Computing Concepts (12 points):** This is the most critical section. Create a dense but highly readable summary of the major themes. Prioritize the concepts that are repeatedly emphasized in the professor's videos:
        *   **Architectures:** Pros and cons of Native, Hybrid-Native (Flutter), Hybrid-Web, and PWA. Focus on the trade-offs.
        *   **Usability:** Key principles like the "Thumb Zone" and the "Fat Finger Problem" (48dp target size).
        *   **Data & Connectivity:** The **Repository Pattern** is crucial. Explain its role in abstracting data sources (API vs. local cache) and enabling offline-first capabilities.
        *   **Autonomy:** Explain the best practices for battery saving. Focus on **batching network requests** and requesting the **lowest necessary GPS precision**.
        *   **Background Tasks:** Explain the OS restrictions and the role of tools like `workmanager` for deferrable, non-urgent tasks.
        *   **Sensors & APIs:** Cover the need for user permissions, the types of sensors, and the role of REST and Auth Tokens.

3.  **Deliver the Final Guide:** Produce the `guia_estudo_exame.md` file. Use formatting like bolding, bullet points, and short paragraphs to make the information easy to scan and transcribe. Where a concept is complex (like the Repository Pattern), you can even describe a simple diagram to be drawn.