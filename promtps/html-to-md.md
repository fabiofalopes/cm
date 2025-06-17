Your task is to act as an expert HTML-to-Markdown converter.

Please follow these rules precisely:

1.  **Create a Slugified Filename:** Take the quiz title provided and convert it into a "slug" for the filename (lowercase, spaces replaced with hyphens, special characters removed). The file should be created in the `resumos/` directory.
2.  **Extract Main Content Only:** Parse the provided HTML and extract only the quiz questions and associated text. You must ignore all irrelevant page elements like `<nav>`, `<header>`, `<footer>`, `<script>`, and `<div>` containers that are not part of the quiz content itself.
3.  **Convert to Clean Markdown:**
    *   Use Markdown headings (`#`, `##`) for titles and questions.
    *   Use lists and other standard Markdown formatting to make the content readable.
4.  **Handle Questions as Fill-in-the-Blanks:**
    *   For questions that require filling in text (`<input type="text">`), use a placeholder like `[ ... ]`.
    *   For multiple-choice questions (`<select>` or radio buttons), list all possible options as a Markdown list with **empty checkboxes**.
    *   **Crucially, do not pre-fill or select any answers**, even if the source HTML has a `selected` or `checked` value. The goal is to create a clean study template.
    *  Give context in the end of the documents where you explain the symbols for completion, for multiple choice keeping the same symbols in the text to represent how to answer if applicable.

**My Request:**

*   **Slugify this name:** `[PASTE THE QUIZ TITLE HERE]`
*   **Convert the following HTML to Markdown:**

```html
[PASTE THE RAW HTML CONTENT HERE]
```
