# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Rails 8.1 application using SQLite3 as the database. It's a product store with user authentication, built using modern Rails conventions including Hotwire (Turbo + Stimulus), Propshaft for assets, and Rails 8's built-in authentication patterns.

**Ruby Version:** 4.0.0

## Common Commands

### Development Server
```bash
bin/dev              # Start development server
bin/rails server     # Start Rails server only
```

### Database
```bash
bin/rails db:create             # Create database
bin/rails db:migrate            # Run pending migrations
bin/rails db:schema:load        # Load schema into database
bin/rails db:seed               # Seed database
bin/rails db:reset              # Drop, create, load schema, and seed
```

### Testing
```bash
bin/rails test                  # Run all tests
bin/rails test test/models      # Run model tests
bin/rails test test/controllers # Run controller tests
bin/rails test:system           # Run system tests
```

### Code Quality
```bash
bin/rubocop          # Run RuboCop linter
bin/brakeman         # Run security scanner
bin/bundler-audit    # Check for vulnerable dependencies
bin/ci               # Run full CI suite locally
```

### Console & Other
```bash
bin/rails console    # Start Rails console
bin/rails routes     # Show all routes
bin/rake             # Run Rake tasks
```

## Architecture Overview

### Authentication System

The app uses Rails 8's recommended authentication pattern with cookie-based sessions:

- **Authentication concern** (app/controllers/concerns/authentication.rb): Provides `require_authentication`, `authenticated?`, session management
- **Controllers** can use `allow_unauthenticated_access only: [:action]` to skip authentication
- **Session model**: Tracks user sessions with user_agent and ip_address
- **Current model**: Thread-safe current session storage
- Sessions stored in signed permanent cookies (`:session_id`)

### Models

- **User**: Has secure password (bcrypt), normalized email, has_many sessions
- **Session**: Belongs to user, tracks IP and user agent
- **Product**: Simple product model with name validation

### Controllers

- **ApplicationController**: Includes Authentication concern, enforces modern browser requirement
- **ProductsController**:
  - Public access: `index`, `show`
  - Authenticated: `new`, `create`, `edit`, `update`, `destroy`
  - Uses `allow_unauthenticated_access` pattern
- **SessionsController**: Handles login/logout
- **PasswordsController**: Password reset functionality

### Views

- Uses partials pattern (e.g., `_form.html.erb`)
- Turbo-enabled forms with `form_with`
- Conditional rendering based on `authenticated?` helper

### Key Rails 8 Patterns

1. **Authentication**: Concern-based with `allow_unauthenticated_access`
2. **Strong parameters**: Uses Rails 8's `params.expect()` syntax
3. **Modern browser requirement**: `allow_browser versions: :modern`
4. **Importmap**: JavaScript via import maps (no bundler)
5. **Propshaft**: Modern asset pipeline
6. **Solid Queue/Cache/Cable**: Database-backed infrastructure

## Development Notes

- All controllers inherit authentication requirement by default; explicitly allow unauthenticated access where needed
- Use `Current.session` to access current user session
- Forms use Turbo by default (no full page reloads)
- The app enforces modern browser support (webp, import maps, CSS nesting, etc.)
