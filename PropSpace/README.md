**Name**: Divine Chinecherem Nnamdi

# PropSpace - Property Listing Application

PropSpace is a full-stack real-time web application where users can list, view, update, and delete properties for rent or sale.

## Main Features
- **Safe Login**: A secure way to sign up and log in using JWT and Bcrypt to keep passwords safe.
- **Manage Listings**: Users can create, view, edit, and delete their own property listings.
- **User Dashboard**: A private space to manage your profile, contact info, and security settings.
- **Search and Filter**: Easily look for properties by city, price range, and type of property.
- **Listing Protection**: Strong backend security makes sure that only the owner of a listing can edit or delete it.
- **Beautiful Design**: A good-looking, mobile-friendly design with dark mode and a modern glass style.

## Tools Used
- **Frontend**: React (using Vite), Axios for getting data, Lucide React for icons, and custom CSS3.
- **Backend**: Node.js and Express.
- **Database**: MongoDB with Mongoose.
- **Security**: JSON Web Tokens (JWT), BcryptJS, and CORS.

## Project Folders
- `client/`: Contains the frontend user interface code.
- `server/`: Contains the backend API code.

## How to Get Started

### What You Need
- Node.js installed on your computer.
- A running MongoDB database (either on your computer or through MongoDB Atlas).

### Setup Guide
1. **Get the Code**: Clone the project or download the files.
2. **Setup the Backend**:
   - Open the server folder: `cd server`
   - Install packages: `npm install`
   - Make a `.env` file with your `PORT`, `MONGO_URI`, and `JWT_SECRET`.
   - Start the server: `node index.js`
3. **Setup the Frontend**:
   - Open the client folder: `cd client`
   - Install packages: `npm install`
   - Start the app: `npm run dev`

## Main API Points

### User Accounts
- `POST /api/users/register`: Create a new user.
- `POST /api/users/login`: Log in a user and get a token.
- `GET /api/users/profile`: Get the logged-in user's profile.
- `PUT /api/users/profile`: Update the user's profile info.

### Property Listings
- `GET /api/properties`: Get all property listings (you can filter by city, type, minPrice, and maxPrice).
- `GET /api/properties/detail/:id`: Get full details about one property.
- `GET /api/properties/mine`: View listings made by the logged-in user.
- `POST /api/properties`: Add a new property listing.
- `PUT /api/properties/:id`: Edit a listing.
- `DELETE /api/properties/:id`: Delete a listing.

## API Error Testing Guide

This guide shows how to check different API responses and errors. You can use tools like Postman to test these on your local computer (`http://localhost:5001/api`).

### 1. 201 Created (Success: User Registered)
- **Method**: `POST`
- **URL**: `/api/users/register`
- **Headers**: `Content-Type: application/json`
- **Body**:
  ```json
  {
    "username": "Tester",
    "email": "test@example.com",
    "password": "password123"
  }
  ```
- **Expected Return**: `201 Created` with a secure JWT token.

### 2. 200 OK (Success: Got Listings)
- **Method**: `GET`
- **URL**: `/api/properties`
- **Expected Return**: `200 OK` with a list of properties.

### 3. 400 Bad Request (Error: Missing Info)
Test this by leaving out required information when creating a listing.
- **Method**: `POST`
- **URL**: `/api/properties`
- **Headers**: `Content-Type: application/json`, `Authorization: Bearer <valid_token>`
- **Body**:
  ```json
  {
    "description": "Missing title and price"
  }
  ```
- **Expected Return**: `400 Bad Request`. Message says `"Missing required fields"`.

### 4. 401 Unauthorized (Error: No Token)
See what happens if you try to view a private page without logging in.
- **Method**: `GET`
- **URL**: `/api/users/profile`
- **Headers**: *(Do not send an Authorization header)*
- **Expected Return**: `401 Unauthorized`. Message says `"Not authorized, no token"`.

### 5. 403 Forbidden (Error: Not Allowed)
Try to change or delete a listing that belongs to someone else.
- **Method**: `DELETE`
- **URL**: `/api/properties/<id_owned_by_account_a>`
- **Headers**: `Authorization: Bearer <token_belonging_to_account_b>`
- **Expected Return**: `403 Forbidden`. Message says `"Unauthorized to delete this listing"`.

### 6. 404 Not Found (Error: Doesn't Exist)
Test what the API does when an item isn't in the database.
- **Method**: `GET`
- **URL**: `/api/properties/detail/64f000000000000000000000` (A fake but validly formatted ID)
- **Expected Return**: `404 Not Found`. Message says `"Property not found"`.
