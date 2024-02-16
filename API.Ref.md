### Authentication Endpoints

#### 1. Register (`/web/auth/register`)

- **Method**: `POST`
- **Request Body**:
  - `fullName`: String (user's full name)
    - Validation: 1-50 characters long
  - `username`: String (chosen username)
    - Validation: 1-20 characters long, alphanumeric
  - `email`: String (user's email address)
    - Validation: Valid email address format `/^[^\s@]+@[^\s@]+\.[^\s@]+$/`
  - `password`: String (user's password)
    - Validation: 8-50 characters long, at least one uppercase, one lowercase, one number, and one special character
  - `confirmPassword`: String (user's password confirmation)
    - Validation: Must match `password`
- **Success Response**:
  - `accessToken`: String (JWT token for authentication)
  - `refreshToken`: String (JWT token for refreshing access token)
- **Description**: Registers new users and provides a session token.

#### 2. Login (`/web/auth/login`)

- **Method**: `POST`
- **Request Body**:
  - `emailOrUsername`: String (email or username of the user)
    - Validation: Should be either email or username
  - `password`: String (user's password)
    - Validation: non-empty,
- **Success Response**:
  - `accessToken`: String (JWT token for authentication)
  - `refreshToken`: String (JWT token for refreshing access token)
- **Description**: Logs in existing users and provides a session token.

#### 3. Session (`/web/auth/session`)

- **Method**: `GET`
- **Success Response**:

  - `user`: Object
    - `id`: String (user's ID)
    - `name`: String (user's full name)
    - `emails`: Object
      - `email`: String (user's email address)
      - `verified`: Boolean (whether the email is verified)
    - `avatar`: String (user's avatar URL)
    - `idp`: String (identity provider)
    - `roles`: Array (user's roles)
  - `createAt`: String (session creation date)
  - `expires`: String (session expiration date)
  - `accessToken`: String (JWT token for authentication)
  - `authProvider`: String (authentication provider)

- **Description**: Retrieves session details of the current user.

#### 4. Email Verification (`/web/auth/verify`)

- **Method**: `POST`
- **Request Body**:
  - `email`: String (user's email)
  - `verificationCode`: String (verification code sent to the email)
- **Success Response**:
  - `message`: String ("Email verified successfully." if successful)
- **Description**: Verifies the user's email address.

#### 5. Resend Verification Email (`/web/auth/resend`)

- **Method**: `POST`
- **Request Body**:
  - `email`: String (user's email)
- **Success Response**:
  - `message`: String ("Email verification message sent successfully." if successful)
- **Description**: Resends the verification email to the user.

#### 6. Refresh Token (`/web/auth/refresh`)

- **Method**: `POST`
- **Request Body**:
  - None
- **Success Response**:
  - `accessToken`: String (JWT token for authentication)
  - `refreshToken`: String (JWT token for refreshing access token)
- **Description**: Refreshes the access token.

### User Management Endpoints

#### 1. User Keys (`/web/users/keys`)

#### **Create**

- **Methods**: `POST`
- **Request Body**:
  - `name`: String (name of the key)
- **Success Response**:
  - `id`: String (key ID)
  - `key`: String (key value)
- **Description**: Creates a new key for the user.

#### **List**

- **Methods**: `GET`
- **Success Response**:
  - `keys`: Array (list of user keys)
- **Description**: Retrieves all keys of the user.

#### **Delete**

- **Methods**: `DELETE`
- **Request Body**:
  - `id`: String (key ID)
- **Success Response**:
  - `message`: String ("Key deleted." if successful)
- **Description**: Deletes a key of the user.

#### **Update**

- **Methods**: `PATCH`
- **Request Body**:
  - `id`: String (key ID)
  - `name`: String (new name of the key)
- **Success Response**:
  - `id`: String (key ID)
  - `name`: String (new name of the key)
- **Description**: Updates the name of a key of the user.

#### 2. User Transactions (`/web/users/me/transactions`)

- **Method**: `GET`
- **Success Response**:
  - `transactions`: Array (list of user transactions)
- **Description**: Retrieves all transactions of the user.

#### 3. Update User (`/web/users/me`)

- **Method**: `PATCH`
- **Request Body**:
  - `name`: String (optional, new full name)
    - Validation: 1-50 characters long
  - `username`: String (optional, new username)
    - Validation: 1-20 characters long, alphanumeric
  - `email`: String (optional, new email)
    - Validation: Valid email address format `/^[^\s@]+@[^\s@]+\.[^\s@]+$/`
  - `oldPassword`: String (optional, old password, required if `password` is provided)
    - Validation: 8-50 characters long, at least one uppercase, one lowercase, one number, and one special character
  - `password`: String (optional, new password)
    - Validation: 8-50 characters long, at least one uppercase, one lowercase, one number, and one special character
  - `confirmPassword`: String (optional, new password confirmation)
    - Validation: Must match `password`
- **Success Response**:
  - `message`: String ("User updated successfully." if successful)
- **Description**: Updates the user's profile.

### General Information

- **Data Format**: JSON
- **Authentication**: Bearer Token (included in the header of authenticated requests)
- **Base URL**: "https://dev-api.pawan.krd"

### Error Handling

- **Error Response**:
  - `status`: Boolean (false)
  - `error`: Object
    - `message`: String (error message)
    - `type`: String (error type)
  - `hint`: String (error hint)
  - `discord`: String (discord server URL)
  - `support`: String (support email address)
- **Description**: Returns an error response.
