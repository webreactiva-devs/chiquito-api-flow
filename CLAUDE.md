# Chiquito API Flow - Claude Code Assistant Guide

## Project Overview

This is **ChiquitoAPIjarl**, a REST API that serves jokes and expressions from the legendary Spanish comedian Chiquito de la Calzada. The project is a lightweight Node.js Express API with JSON file-based data storage.

## Technology Stack

- **Runtime**: Node.js >= 21.0.0 with ES modules
- **Framework**: Express.js 4.18.2
- **CORS**: Enabled without restrictions (cors 2.8.5)
- **Data Storage**: JSON file (`/Users/daniel/Sites/lab/claude-code-workshop/code/chiquito-api-flow/data/chiquito.json`)
- **Testing**: Node.js built-in test runner with Supertest
- **Documentation**: OpenAPI 3.0.4

## Project Architecture

### File Structure
```
/Users/daniel/Sites/lab/claude-code-workshop/code/chiquito-api-flow/
├── src/
│   ├── app.js      # Express app configuration and routes
│   └── server.js   # Server initialization
├── data/
│   └── chiquito.json # Jokes database (17 jokes across 5 categories)
├── tests/
│   └── app.test.js   # Comprehensive test suite
├── docs/
│   └── openapi.yml   # API documentation
├── .github/
│   ├── workflows/    # CI/CD, deployment, monitoring
│   ├── copilot-instructions.md # Code style guide
│   ├── dependabot.yml # Dependency management
│   └── templates/    # Issue and PR templates
└── package.json     # Project configuration
```

### Entry Points
- **Main server**: `/Users/daniel/Sites/lab/claude-code-workshop/code/chiquito-api-flow/src/server.js`
- **App configuration**: `/Users/daniel/Sites/lab/claude-code-workshop/code/chiquito-api-flow/src/app.js`
- **Data source**: `/Users/daniel/Sites/lab/claude-code-workshop/code/chiquito-api-flow/data/chiquito.json`

## API Endpoints

### Core Endpoints
- `GET /health` - Health check with Chiquito-style response
- `GET /api/jokes` - Get all jokes (supports `?category=` filter)
- `GET /api/jokes/random` - Get a random joke
- `GET /api/jokes/:id` - Get specific joke by ID
- `GET /api/categories` - Get all categories with joke counts

### Data Model
```json
{
  "id": 1,
  "type": "phrase|joke",
  "content": "Joke or phrase content",
  "category": "Category name"
}
```

### Available Categories
- clásico (10 jokes)
- crisis (1 joke)
- comparaciones (2 jokes)
- absurdo (2 jokes)
- familia (2 jokes)

## Development Workflow

### Scripts
```bash
npm start     # Production server (node src/server.js)
npm run dev   # Development with auto-reload (node --watch src/server.js)
npm test      # Run test suite (node --test tests/*.test.js)
```

### Development Server
- Default port: 3000
- Environment variable: `PORT`
- Auto-reload in development mode

## Code Style Guidelines (MANDATORY)

### Strict Rules
1. **NO inline comments allowed** - Code must be self-documenting
2. **All code descriptions in English** - Variables, functions, documentation
3. **Descriptive naming** - Use clear, meaningful names
4. **Modern JavaScript** - ES6+ features, ES modules
5. **Clean patterns** - Small, focused functions

### Examples
```javascript
// ✅ GOOD
const getRandomJoke = (jokes) => {
  return jokes[Math.floor(Math.random() * jokes.length)];
};

// ❌ BAD
const joke = jokes[Math.floor(Math.random() * jokes.length)]; // Gets random joke
```

## Testing

### Test Coverage
- All API endpoints tested
- Error handling (404, 500)
- Category filtering
- Data validation
- Response format verification

### Test Runner
- Uses Node.js built-in test runner
- Supertest for HTTP testing
- Located at: `/Users/daniel/Sites/lab/claude-code-workshop/code/chiquito-api-flow/tests/app.test.js`

## CI/CD & Deployment

### GitHub Actions Workflows
- **CI**: `/Users/daniel/Sites/lab/claude-code-workshop/code/chiquito-api-flow/.github/workflows/ci.yml`
- **Deploy**: `/Users/daniel/Sites/lab/claude-code-workshop/code/chiquito-api-flow/.github/workflows/deploy.yml`
- **Monitor**: `/Users/daniel/Sites/lab/claude-code-workshop/code/chiquito-api-flow/.github/workflows/monitor.yml`

### Dependency Management
- Dependabot configured for npm updates
- Node.js >= 21.0.0 required

## Error Handling

### Error Response Format
```json
{
  "error": "Error message, fistro"
}
```

### Status Codes
- 200: Success
- 404: Resource not found
- 500: Server error

## Key Implementation Details

### Data Loading
- JSON data loaded synchronously at startup
- Data cached in memory for performance
- Located at: `/Users/daniel/Sites/lab/claude-code-workshop/code/chiquito-api-flow/data/chiquito.json`

### Category Processing
- Dynamic category counting from jokes data
- No hardcoded category list
- Built-in aggregation function: `buildCategoriesWithCount()`

### CORS Configuration
- Enabled for all origins
- No restrictions on headers or methods

## Documentation

### API Documentation
- OpenAPI 3.0.4 specification
- Complete endpoint documentation with examples
- Schema definitions for all models
- Located at: `/Users/daniel/Sites/lab/claude-code-workshop/code/chiquito-api-flow/docs/openapi.yml`

### Existing Instructions
- GitHub Copilot instructions: `/Users/daniel/Sites/lab/claude-code-workshop/code/chiquito-api-flow/.github/copilot-instructions.md`
- README.md with comprehensive setup and usage guide

## Working with This Codebase

### When Adding Features
1. Follow the existing REST patterns in `/Users/daniel/Sites/lab/claude-code-workshop/code/chiquito-api-flow/src/app.js`
2. Add corresponding tests to `/Users/daniel/Sites/lab/claude-code-workshop/code/chiquito-api-flow/tests/app.test.js`
3. Update OpenAPI documentation in `/Users/daniel/Sites/lab/claude-code-workshop/code/chiquito-api-flow/docs/openapi.yml`
4. Ensure no inline comments are added

### When Modifying Data
- Edit `/Users/daniel/Sites/lab/claude-code-workshop/code/chiquito-api-flow/data/chiquito.json`
- Maintain the existing data structure
- Ensure IDs are sequential and unique
- Categories are automatically aggregated

### When Debugging
- Check server startup logs
- Use the `/health` endpoint for basic connectivity
- All errors include "fistro" for consistency with the theme

## Performance Characteristics

- **Startup**: Data loaded once at application start
- **Memory**: All jokes cached in memory (~17 jokes)
- **Concurrency**: Standard Express.js handling
- **Response Time**: Sub-millisecond for cached data operations

## Security Considerations

- CORS enabled for all origins (development-friendly)
- No authentication or rate limiting
- Input validation on ID parameters (integer parsing)
- No file system write operations (read-only data)

This API is designed for simplicity and educational purposes, focusing on clean code patterns and comprehensive testing rather than enterprise-grade security features.
- No quiero que añadas información de Claude o Anthropic en el mensaje de commit. No quiero esto:    🤖 Generated with [Claude Code](https://claude.ai/code)                                         │
│                                                                                                   │
│   Co-Authored-By: Claude <noreply@anthropic.com>"