# testing
# Generate a Pydantic model for the incoming JSON body with a single field "text"
from pydantic import BaseModel

class TextRequest(BaseModel):
    text: str
import hashlib
from fastapi import FastAPI
from pydantic import BaseModel
from fastapi.responses import JSONResponse

app = FastAPI()

class TextRequest(BaseModel):
    text: str

@app.post("/generate-checksum/")
async def generate_checksum(request: TextRequest):
    # Compute the checksum (MD5 hash) of the provided text
    checksum = hashlib.md5(request.text.encode()).hexdigest()
    return JSONResponse(content={"checksum": checksum})
@app.get("/")
async def welcome():
    return {"message": "Welcome to the API! Developed by [Your Name]."}
@app.post("/generate-checksum/")
async def generate_checksum(request: TextRequest):
    """
    Endpoint to generate a checksum (MD5 hash) of the provided text.

    - **request**: A JSON body containing the text for which the checksum will be generated.
    - **Returns**: A JSON object with the computed checksum of the provided text.

    Example:
    - Request Body: {"text": "hello"}
    - Response: {"checksum": "5d41402abc4b2a76b9719d911017c592"}
    """
    # Compute the checksum (MD5 hash) of the provided text
    checksum = hashlib.md5(request.text.encode()).hexdigest()
    return JSONResponse(content={"checksum": checksum})
from fastapi.testclient import TestClient
from main import app  # Assuming your FastAPI app is in main.py

client = TestClient(app)

def test_generate_checksum():
    # Test with a valid text input
    response = client.post("/generate-checksum/", json={"text": "hello"})
    assert response.status_code == 200
    assert response.json() == {"checksum": "5d41402abc4b2a76b9719d911017c592"}

    # Test with an empty text input
    response = client.post("/generate-checksum/", json={"text": ""})
    assert response.status_code == 200
    assert response.json() == {"checksum": "d41d8cd98f00b204e9800998ecf8427e"}
from fastapi import HTTPException
from typing import Any

@app.post("/generate-checksum/")
async def generate_checksum(request: TextRequest) -> dict[str, Any]:
    ...
# FastAPI Checksum Generator

This is a FastAPI application that provides an endpoint to generate an MD5 checksum for a given text.

## Requirements

- Python 3.7+
- Install dependencies: `pip install -r requirements.txt`

## Running the Application

To run the application, use Uvicorn:

```bash
uvicorn main:app --reload
{
  "text": "string"
}
{
  "checksum": "string"
}

### Summary

By following the steps above, you’ve:

- Created a FastAPI endpoint that accepts a `POST` request and computes a checksum for the provided text.
- Added a welcome message with your name.
- Documented the new API endpoint.
- Added test cases for the new endpoint.
- Provided a `README.md` file for running the application.

Each step is broken down clearly to guide both the development and testing of the FastAPI application.
