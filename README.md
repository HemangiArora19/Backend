# Backend API Documentation

## Base URL

```
http://localhost:8000
```

---

## Authentication

### JWT-based Authentication Header

All protected routes require:

```
Authorization: Bearer <access_token>
```

---

## User Routes

### POST `/create-account`

**Description:** Register a new user

**Body:**

```json
{
  "fullName": "John Doe",
  "email": "john@example.com",
  "password": "securePassword"
}
```

**Response:**

* 201 Created: User registered successfully

### POST `/login`

**Description:** Log in an existing user

**Body:**

```json
{
  "email": "john@example.com",
  "password": "securePassword"
}
```

**Response:**

* 200 OK: Login successful

### GET `/get-user`

**Description:** Retrieve logged-in user's data

**Headers:** Authorization required

**Response:**

* 200 OK: Returns user details

---

## Travel Story Routes

### POST `/add-travel-story`

**Description:** Add a new travel story

**Body:**

```json
{
  "title": "Trip to Bali",
  "story": "Great adventure!",
  "visitedLocation": "Bali",
  "imageUrl": "http://...",
  "visitedDate": "timestamp in ms"
}
```

**Response:**

* 201 Created: Story added

### GET `/get-all-stories`

**Description:** Get all travel stories of logged-in user

**Response:**

* 200 OK: List of stories

### POST `/edit-story/:id`

**Description:** Edit a specific story

**Body:**

```json
{
  "title": "Updated Title",
  "story": "Updated story",
  "visitedLocation": "Updated location",
  "imageUrl": "http://...",
  "visitedDate": "timestamp in ms"
}
```

**Response:**

* 200 OK: Story updated

### DELETE `/delete-story/:id`

**Description:** Delete a specific story

**Response:**

* 200 OK: Story deleted

---

## Image Routes

### POST `/image-upload`

**Description:** Upload an image (form-data field: `image`)

**Response:**

* 200 OK: Returns image URL

### DELETE `/delete-image?imageUrl=...`

**Description:** Delete an image using imageUrl

**Response:**

* 200 OK: Image deleted

---

## Story Features

### PUT `/update-is-favourite/:id`

**Description:** Update the isFavourite flag of a story

**Body:**

```json
{
  "isFavourite": true
}
```

**Response:**

* 200 OK: Favourite updated

### GET `/search?query=...`

**Description:** Search stories by title, story content, or location

**Response:**

* 200 OK: Search results

### GET `/travel-stories/filter?startDate=...&endDate=...`

**Description:** Filter stories by visited date (in milliseconds)

**Response:**

* 200 OK: Filtered stories

---

## Static File Access

### `/uploads/<filename>`

* Access uploaded images

### `/assets/<filename>`

* Access other static assets

---

## Environment Variables (Required)

```
PORT=8000
MONGO_URI=<MongoDB connection string>
ACCESS_TOKEN_SECRET=<JWT secret>
```

---

## Models Used

### User Model (user.models.js)

* fullName: String
* email: String
* password: Hashed String

### Travel Story Model (travelStory.model.js)

* title: String
* story: String
* visitedLocation: String
* imageUrl: String
* visitedDate: Date
* userId: ObjectId
* isFavourite: Boolean (default: false)

---

## Middleware

* `authenticateToken`: Verifies JWT
* `upload`: Handles image upload (using multer)

---

## Notes

* All dates must be passed as timestamps (milliseconds).
* Image filenames are automatically generated and stored in the `/uploads` folder.
