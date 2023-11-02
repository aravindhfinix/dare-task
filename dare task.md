# Dare App Documentation

## User Module

### User Signup

#### User Authentication

The user must authenticate using their email and password for registration.

#### User Registration

- **Request:**
  - `email` (string)
  - `full_name` (string)
  - `kyc_documents` (array of image URLs, 2 images required)
  - `profile_image` (image URL)
  - `gender` (string)
  - `date_of_birth` (date)
  - `password` (string)

- **Response:**
  - Send an OTP for email verification.

#### User Email Verification

- **Request:**
  - `email` (string)
  - `otp` (string)

- **Response:**
  - If OTP is verified, change the user's status to 'approved.'
  - If OTP is invalid, return an error message.

#### User Login

- **Request:**
  - `email` (string)
  - `password` (string)

- **Response:**
  - Check the user's status. If 'waiting,' send: "Waiting for admin's approval."
  - If approved, generate an authentication token for the user.

## Admin Module

### Admin Login

#### Admin Authentication

The administrator must authenticate using proper credentials to access their admin privileges.

#### Admin Login

- **Request:**
  - `email` (string)
  - `password` (string)

- **Response:**
  - If credentials are valid, generate an authentication token for the admin.

#### Admin View KYC Documents

- **Response:**
  - Return a list of users in 'waiting' status with their KYC documents.

#### Admin Approve/Reject User

- **Request:**
  - `userId` (string)

- **Response:**
  - Admin can approve or reject a user.
  - If rejected, increment the rejection_count.
  - If rejection_count reaches 3, permanently ban the user.

## User Module (Post-Approval)

#### Add Friends

Add friends to the user's friend list.

#### Create Dares

- **Request:**
  - `dare_name` (string)
  - `suggested_to` (array of user IDs)

- **Response:**
  - Create dares with 'pending' status.

#### Suggest Dare to Friend

- **Request:**
  - `dare_id` (string)
  - `friend_id` (string)

- **Response:**
  - Suggest dares to friends.

#### Mark Dare as Completed

Mark a dare as completed.

#### Edit/Delete Dares

Users can edit or delete dares they've created.

#### Filter Dares

- **Request:**
  - Filter parameters (time & date, friends, dare_name)

- **Response:**
  - Return filtered dares.

#### List Previous Day Pending Dares

Get a list of dares that are pending from the previous day.

### Email Notifications

#### End of Day (EOD) Email

Scheduled to trigger at the end of the day, sending emails with lists of completed and pending dares for each friend.



### Additional Considerations

- **Proper Authentication**: Implement secure authentication mechanisms to ensure user data privacy and security.
- **Data Validation**: Apply data validation to maintain data consistency and security.
- **Documentation**: Create comprehensive API documentation for both internal and external use.
- **Folder and Code Structure**: Maintain a well-organized codebase with clear folder structure for easy management.
- **Security**: Implement proper security measures, such as encryption of sensitive data.
- **Scalability**: Design the application to handle an increasing number of users and tasks.
- **Performance**: Optimize API calls for efficient performance.
