# IT-SPRINT1-MAQUETACIO

## Description

I have created this webpage to practice CSS elements such as CSS Grid, CSS Flexbox, accesibility, SEO and good overall HTML and CSS practices.
It includes a header, a main element and a footer, each designed to resemble what a real website could look like, with buttons and images.

## Preview

![Preview](src/assets/img/Readme.png)

## Project Structure

```
/
├── index.html          # Main page
├── src/
│   ├── css/
│   │   └── style.css   # CSS styles
│   └── assets/
│       ├── img/        # Project images
│       └── icons/      # Icons
├── recommendations/    # Best practices documentation
├── .gitignore
└── README.md
```
This project has a particular git branching strategy, so each iteration should be developed on a separate feature-branch. Each branch should maintain a separated README.md file with specific instructions related to the tecnologies used in that iteration. The sugestion for the branch structure in this project is:

```
/
└── main
    └── develop
        ├── vainilla-iteration 
            ├── feature/navbar
            ├── feature/footer
            ├── feature/form
            ├── feature/desktop-styling
            └── feature/...
        ├── sass-iteration
            └── feature/...
        └── tailwind-iteration               // Remember to use npm o pnpm to develop easy and faster in this iteration. Also remember add to the .gitignore the node-modules folder
            └── feature/...

```
## BECAREFUL!
From this section of the readme you should write in base on the tecnology context selected.

## Technologies Used

- **HTML5** - Semantic structure
- **CSS3** - Styles and responsive design
- **Tailwind** - Styling library (just add this )
- **GitHub Pages** (optional) - Deployment

## Installation and Execution

### Prerequisites

- A modern web browser (Chrome, Firefox, Edge, Safari)
- A code editor (recommended: VS Code)
- Git installed (optional but recommended)

### Steps to run the project

1. **Clone the repository** (or download the ZIP):
```bash
git clone https://github.com/your-username/your-repository.git
```

2. **Navigate to the project folder**:
```bash
cd your-repository
```

3. **Open the HTML file in your browser**:
   - Option 1: Double-click on `index.html`
   - Option 2: Use Live Server in VS Code (recommended)

### Using Live Server in VS Code (recommended)

1. Install the [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) extension
2. Right-click on `index.html`
3. Select "Open with Live Server"

## Usage

Customize the project by editing:
- `index.html` - Modify content and structure
- `src/css/style.css` - Change styles and colors
- `src/assets/` - Add your own images and icons

## Contributors

- **Albert Muntal Perez** - [Dr.Munty](https://github.com/DrMunty)

## License

This project is under the MIT License - see the [LICENSE](LICENSE) file for more details.

---

If you liked this project, give it a star on GitHub