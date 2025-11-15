---
description: Generate and update API documentation
---

Generate or update API documentation for the rental API platform.

Perform the following:

1. **Review OpenAPI/Swagger docs**:
   - Start backend server if not running
   - Access FastAPI auto-generated docs at http://localhost:8000/docs
   - Check completeness of endpoint documentation

2. **Verify documentation coverage**:
   - Check all endpoints have descriptions
   - Verify request/response schemas are documented
   - Check examples are provided
   - Verify error responses are documented

3. **Check Pydantic schemas**:
   - Review schemas in `backend/app/schemas/`
   - Ensure all fields have descriptions
   - Check Field(..., description="...") is used
   - Verify examples are provided

4. **Update README documentation**:
   - Verify API endpoints are listed in backend/README.md
   - Check example requests are up-to-date
   - Verify authentication examples work

5. **Generate additional documentation** (if needed):
   - API changelog
   - Migration guide
   - Integration examples
   - SDK documentation

Provide:
- Documentation coverage report
- Missing documentation items
- Suggestions for improvement
- Updated documentation files (if requested)
