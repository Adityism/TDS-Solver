# TDS Solver API

An API for automatically solving graded assignment questions from IIT Madras' Online Degree in Data Science course.

## Features

- Accepts any question from the graded assignments
- Processes uploaded files (CSV, ZIP, etc.)
- Returns concise answers ready for submission
- Easy to deploy on Vercel or other platforms

## API Usage

The API accepts POST requests with multipart/form-data:

```bash
curl -X POST "https://your-app.vercel.app/api/" \
  -H "Content-Type: multipart/form-data" \
  -F "question=Download and unzip file abcd.zip which has a single extract.csv file inside. What is the value in the \"answer\" column of the CSV file?" \
  -F "file=@abcd.zip"
```

Response:

```json
{
  "answer": "1234567890"
}
```

## API Documentation

### Endpoint: POST /api/

The API accepts questions and optional file attachments through multipart/form-data requests.

#### Request Format

- Content-Type: `multipart/form-data`
- Method: `POST`

#### Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| question  | text | Yes | The assignment question to answer |
| file      | file | No  | File attachment (CSV, ZIP, etc.) |

#### Example Requests

1. Simple question without file:
```bash
curl -X POST "https://your-app.vercel.app/api/" \
  -H "Content-Type: multipart/form-data" \
  -F "question=What is 2+2?"
```

2. Question with CSV file:
```bash
curl -X POST "https://your-app.vercel.app/api/" \
  -H "Content-Type: multipart/form-data" \
  -F "question=What is the mean of column A?" \
  -F "file=@data.csv"
```

#### Response Format

```json
{
  "answer": "string"
}
```

#### Error Responses

```json
{
  "error": "Error message description"
}
```

Common HTTP status codes:
- 200: Success
- 400: Bad Request
- 415: Unsupported Media Type
- 500: Internal Server Error

## Setup Instructions

1. Clone this repository
2. Create a `.env` file with your AI Proxy Token:
   ```
   AI_PROXY_TOKEN=your_token_here
   AI_PROXY_URL=https://api.openai.com/v1/chat/completions
   ```
3. Install dependencies:
   ```
   pip install -r requirements.txt
   ```
4. Run the app:
   ```
   python app.py
   ```

## Deployment

### Vercel Deployment

1. Fork this repository
2. Connect to Vercel
3. Add environment variables:
   - `AI_PROXY_TOKEN`
   - `AI_PROXY_URL`
4. Deploy

### Other Platforms

The application can also be deployed on Render, Railway, or any other platform that supports Python applications.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Deployment Instructions

To deploy your TDS Solver API application, follow these steps:

### Step 1: Prepare Your Repository

1. Create a new public GitHub repository
2. Upload all the files I've provided:
   - `app.py`
   - `requirements.txt`
   - `vercel.json`
   - `.env` (remember to add your actual token)
   - `LICENSE` (MIT License)
   - `README.md`

### Step 2: Set Up Environment Variables

1. **Important**: Make sure to edit the `.env` file with your actual AI Proxy Token:
   ```
   AI_PROXY_TOKEN=your_actual_token_here
   AI_PROXY_URL=https://api.openai.com/v1/chat/completions
   ```

2. **Note**: Don't commit this file to GitHub to avoid exposing your token. Instead, you'll set these variables in your deployment platform.

### Step 3: Deploy to Vercel

1. Create a Vercel account if you don't have one: [https://vercel.com/signup](https://vercel.com/signup)
2. Install the Vercel CLI (optional):
   ```
   npm install -g vercel
   ```
3. From the Vercel dashboard:
   - Click "Add New" → "Project"
   - Connect to your GitHub repository
   - Under "Environment Variables", add:
     - `AI_PROXY_TOKEN`: Your actual token
     - `AI_PROXY_URL`: The API URL for your AI service
   - Click "Deploy"
