# Nucampsite Full Stack  
MongoDB Atlas + Google Cloud Functions + Firebase Hosting

Full-stack cloud deployment of the Nucampsite application using React, Express, MongoDB Atlas, Google Cloud Functions (1st Gen), and Firebase Hosting.

---

## Architecture

Client (Firebase Hosting)  
⬇  
Express API (Google Cloud Function)  
⬇  
MongoDB Atlas  

---

## Server Configuration

Create a `config.js` file in the server root directory:

```js
module.exports = {
  secretKey: 'yourSecretKey',
  mongoConnectionString: 'yourMongoAtlasConnectionString',
  bucketName: 'yourGoogleCloudStorageBucket'
};
```

Install dependencies:

```bash
npm ci
```

Test locally:

```bash
npx @google-cloud/functions-framework --target=nucampsiteServer
```

Verify:

```
http://localhost:8080/campsites
```

---

## Deploy Backend (Google Cloud Functions – 1st Gen)

```bash
gcloud auth login
gcloud config set project YOUR_PROJECT_ID
gcloud functions deploy nucampsiteServer \
  --trigger-http \
  --runtime=nodejs20 \
  --allow-unauthenticated \
  --no-gen2
```

Verify deployment:

```
https://your-cloud-function-url/campsites
```

---

## Frontend Configuration

Update:

```
src/app/shared/baseUrl.js
```

```js
export const baseUrl = 'https://your-cloud-function-url/';
```

Ensure the URL ends with a trailing slash.

---

## Deploy Frontend (Firebase)

```bash
npm run build
firebase deploy
```

Add your Firebase hosting URL to the backend CORS whitelist and redeploy the function.

---

## Security

Do **not** commit:
- MongoDB connection strings  
- JWT secrets  
- Cloud storage credentials  

Use environment variables for production environments.

---

## Stack

Node.js • Express • Mongoose • MongoDB Atlas • Passport (Local + JWT) • Google Cloud Functions • Firebase Hosting • React • Redux Toolkit

---

Deployed architecture demonstrates full client–server cloud integration with authentication, database persistence, and serverless infrastructure.
