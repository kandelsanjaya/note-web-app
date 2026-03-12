# Simple Notes App - PHP CRUD Application

A beginner-friendly notes application built with PHP and PostgreSQL demonstrating fundamental web development concepts.

## Live Demo

🔗 **[https://simple-notes-php.onrender.com](https://simple-notes-php.onrender.com)**

## Tech Stack

| Technology | Purpose |
|------------|---------|
| **PHP 8.2** | Backend language |
| **PostgreSQL** | Database (via Supabase) |
| **PDO** | Database abstraction layer |
| **HTML5/CSS3** | Frontend markup & styling |
| **CSS Variables** | Dark/Light theme support |
| **Docker** | Containerization for deployment |
| **Apache** | Web server (in Docker) |

## Features

- **User Authentication**: Register, Login, Logout with session-based auth
- **User-Specific Notes**: Each user sees only their own notes
- Create, Read, Update, Delete (CRUD) notes
- Pin important notes to the top
- Archive notes for later
- Search notes by title or content
- Color-coded notes
- Categorize notes (Personal, Work, Ideas, Shopping, Important)
- Dark/Light theme toggle
- Responsive design
- Secure password hashing with `password_hash()`

## Project Structure

```
notesapp/
├── config/
│   └── database.php      # Database connection & auto-initialization
├── includes/
│   ├── header.php        # HTML header, navigation, session, theme toggle
│   ├── footer.php        # HTML footer
│   ├── functions.php     # Helper functions (CRUD, validation & auth)
│   ├── noteform.php      # Reusable note form partial (shared by create & edit)
│   └── env_loader.php    # .env file loader
├── css/
│   └── style.css         # Styling (with dark mode support)
├── images/
│   ├── login-illustration.svg
│   └── register-illustration.svg
├── index.php             # Home page - List all notes
├── note.php              # Note controller: Create / Edit / Delete
├── search.php            # Search results page
├── archive.php           # View/manage archived notes
├── register.php          # User registration page
├── login.php             # User login page
├── logout.php            # Logout handler
├── test_db.php           # Database connection test script
├── Dockerfile            # Docker configuration for deployment
├── .env                  # Environment variables (DB credentials)
└── README.md             # This file
```

## Requirements

- PHP 8.0 or higher
- PDO with PostgreSQL driver (`php-pgsql`)
- A PostgreSQL database (e.g. [Supabase](https://supabase.com) free tier)
- Web server (Apache, Nginx, or PHP built-in server)
- A `.env` file with your `DATABASE_URL`

## Installation (Local Development)

1. Clone or download this project
2. Navigate to the project directory
3. Start the PHP built-in server:
   ```bash
   php -S localhost:8000
   ```
4. Open `http://localhost:8000` in your browser

The database will be automatically created with sample categories on first run.

## Deployment (Docker/Render.com)

### Using Docker locally:
```bash
docker build -t notesapp .
docker run -p 8000:10000 -e PORT=10000 notesapp
```

### Deploy to Render.com:
1. Push code to GitHub
2. Connect repo to Render.com
3. It will auto-detect the Dockerfile and deploy

## What to Code First (Recommended Order)

If you're building this from scratch, follow this order:

```
1. config/database.php          → Database connection first
2. includes/env_loader.php      → Load .env variables
3. includes/functions.php       → Helper functions (sanitize, redirect, flash, validateNoteInput)
4. includes/header.php          → Common HTML header & navigation
5. includes/footer.php          → Common HTML footer
6. css/style.css                → Basic styling
7. index.php                    → Read notes (the "R" in CRUD)
8. includes/noteform.php        → Reusable form partial
9. note.php                     → Create / Edit / Delete (C, U, D in CRUD) — single controller
10. search.php                  → Search functionality
11. archive.php                 → Archive feature
12. register.php                → User registration
13. login.php                   → User login
14. logout.php                  → Logout handler
```

## Troubleshooting

### Categories not showing in dropdown
**Problem**: Category dropdown is empty when creating/editing notes.

**Solution**: The database needs to be reinitialized. Delete the `data/notes.db` file and refresh the page. Categories will be auto-created.

```bash
rm data/notes.db
```

### Database connection failed
**Problem**: Error "Database connection failed" on page load.

**Solution**:
1. Ensure `data/` directory exists and is writable
2. Check PHP has SQLite extension: `php -m | grep sqlite`
3. On Linux/Mac: `chmod 775 data/`

### Session/Login issues
**Problem**: Can't stay logged in or session errors.

**Solution**:
1. Ensure `session_start()` is called before any output
2. Check PHP session directory is writable
3. Clear browser cookies and try again

### Docker container won't start
**Problem**: Container exits immediately or port issues.

**Solution**:
```bash
# Check logs
docker logs <container_id>

# Ensure port is available
docker run -p 8080:10000 -e PORT=10000 notesapp
```

### Notes not showing after login
**Problem**: User logs in but s
