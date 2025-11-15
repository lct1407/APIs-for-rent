# API Testing Skill

**Description**: Test FastAPI endpoints with comprehensive test coverage

**When to use**: When you need to test API endpoints, verify responses, or debug API issues

## Instructions

When invoked, you should:

1. **Analyze the endpoint** you're testing:
   - Read the relevant router file in `backend/app/api/v1/`
   - Understand the endpoint's parameters, body schema, and expected responses
   - Check the corresponding Pydantic schemas in `backend/app/schemas/`

2. **Check existing tests**:
   - Look in `backend/tests/` for existing test files
   - Identify gaps in test coverage

3. **Set up test environment**:
   - Ensure test database is configured
   - Check if fixtures are needed
   - Verify authentication requirements

4. **Write/run tests**:
   ```bash
   # Run specific test file
   cd backend && pytest tests/test_<module>.py -v

   # Run with coverage
   pytest tests/test_<module>.py --cov=app.<module> --cov-report=term-missing

   # Run all tests
   pytest -v
   ```

5. **Test categories to cover**:
   - **Happy path**: Valid inputs, expected outputs
   - **Authentication**: Token validation, permission checks
   - **Validation**: Invalid inputs, missing fields
   - **Edge cases**: Boundary values, empty data
   - **Error handling**: 404s, 400s, 500s
   - **Rate limiting**: If applicable
   - **Database state**: Check data persistence

6. **Common test patterns**:

```python
import pytest
from httpx import AsyncClient
from app.main import app

@pytest.mark.asyncio
async def test_create_item(client: AsyncClient, auth_headers: dict):
    """Test creating a new item"""
    payload = {
        "name": "Test Item",
        "description": "Test description"
    }

    response = await client.post(
        "/api/v1/items",
        json=payload,
        headers=auth_headers
    )

    assert response.status_code == 201
    data = response.json()
    assert data["name"] == payload["name"]
    assert "id" in data

@pytest.mark.asyncio
async def test_get_item_not_found(client: AsyncClient, auth_headers: dict):
    """Test getting non-existent item"""
    response = await client.get(
        "/api/v1/items/999999",
        headers=auth_headers
    )

    assert response.status_code == 404

@pytest.mark.asyncio
async def test_unauthorized_access(client: AsyncClient):
    """Test endpoint requires authentication"""
    response = await client.get("/api/v1/items")
    assert response.status_code == 401
```

7. **Report results**:
   - Show test output
   - Report coverage percentage
   - Highlight any failures
   - Suggest improvements

## Available Test Fixtures

Common fixtures you can use (check `backend/tests/conftest.py`):
- `client`: Async HTTP client
- `db_session`: Database session
- `auth_headers`: Authentication headers
- `test_user`: Test user instance
- `test_admin`: Test admin user instance

## Tips

- Always clean up test data after tests
- Use transactions for test isolation
- Mock external services (Stripe, PayPal, email)
- Test both sync and async code paths
- Check WebSocket connections if testing WS endpoints

## Output

Provide:
1. Test results summary
2. Coverage report
3. Any failed tests with debugging info
4. Recommendations for additional tests
