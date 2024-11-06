# Laravel precognition with sveltekit

This is a simple example of how to use Laravel as a backend and SvelteKit as a frontend.

## Installation

1. Clone the repository
 ```bash
    git clone git@github.com:renatomoor/sveltekit-precognition.git
```

2. Create a `.env` file
```bash
    cp .env.example .env
```

3. Install the dependencies
```bash
    cd sveltekit-precognition
    composer install
    cd frontend && pnpm install
```

4. Generate the application key
```bash
    # go back to the root of the project and run
    php artisan key:generate
```

5. Run the migrations
```bash
    php artisan migrate
```

6. Run the development servers
```bash
    composer dev
```

7. Access the frontend application
```bash
    http://localhost:5173/
```
