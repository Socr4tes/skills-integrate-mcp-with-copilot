# Feature Enhancement Issues for Mergington High School Activities

Copy and paste each issue below into your GitHub repository's "New Issue" form.

---

## Issue 1: Add User Authentication & Registration System

**Labels:** `enhancement`, `authentication`, `high-priority`

### Description

Implement a complete user authentication and registration system to replace the simple email-based identification.

### Proposed Features

- **User Registration** with comprehensive profile creation:
  - First name and last name
  - Email address (unique identifier)
  - Password with encryption (BCrypt)
  - Phone number (10-digit validation)
  - Physical address
  - Birthday
- **JWT-based Authentication** for secure session management
- **Login/Logout** functionality with token generation
- **Role-Based Access Control** with three user types:
  - **STUDENT**: Browse activities and request to join
  - **CLUB_ADMIN**: Manage specific club(s)
  - **SUPER_ADMIN**: Full system administration
- **Protected API routes** based on authentication status
- **Password reset** functionality (optional for v1)

### Benefits

- Enhanced security with encrypted passwords
- Personalized user experience
- Foundation for advanced features like user profiles and activity history
- Proper authorization for admin functions

### Technical Requirements

- JWT token generation and validation libraries (e.g., PyJWT)
- Password hashing with BCrypt or Passlib
- Session/token management
- Middleware for protected routes
- Input validation for all user data

---

## Issue 2: Implement Request/Approval Workflow System

**Labels:** `enhancement`, `workflow`, `high-priority`

### Description

Replace instant sign-ups with a request-based workflow where students request to join activities and admins approve or reject them.

### Proposed Features

- **Request Submission**:
  - Students submit requests with a comment explaining their interest
  - Automatic status tracking (PENDING → APPROVED/REJECTED)
  - Request timestamps for created and updated dates

- **Admin Request Management**:
  - Dashboard to view all pending requests for their activities
  - Approve requests (adds student to activity)
  - Reject requests with optional feedback comment
  - View request history

- **Request Status Tracking**:
  - Students can view all their requests and statuses
  - Email notifications on status changes (optional)
  - Request cannot be resubmitted if one is pending

### Business Rules

- Duplicate prevention: Can't submit multiple requests for same activity
- Capacity enforcement: Can't approve if activity is full
- Student limit: Students can join maximum 3 activities
- Only club admins can approve/reject for their activities

### Database Changes

Add `club_requests` table with:
- request_id, user_id, activity_id, comment, status, created_at, updated_at, admin_comment

---

## Issue 3: Add Announcements & Events System

**Labels:** `enhancement`, `communication`, `medium-priority`

### Description

Enable club admins to post announcements and events to keep members informed about club activities.

### Proposed Features

- **Create Announcements**:
  - Title and content
  - Two types: ANNOUNCEMENT or EVENT
  - Timestamp tracking
  - Rich text support (optional)

- **View Announcements**:
  - Students see announcements from activities they've joined
  - Display on dashboard with most recent first
  - Click to expand full announcement

- **Authorization**:
  - Club admins can only post for their own activities
  - Super admins can post to any activity
  - Students can only view (no posting)

### Benefits

- Improved communication between admins and members
- Event scheduling and coordination
- Keeps members engaged and informed

### Database Changes

Add `announcements` table with:
- announcement_id, activity_id, posted_by_user_id, title, content, type, created_at, updated_at

---

## Issue 4: Build Q&A / Discussion Forum for Activities

**Labels:** `enhancement`, `community`, `medium-priority`

### Description

Create a Q&A forum where activity members can ask questions and get answers from other members.

### Proposed Features

- **Questions**:
  - Members can post questions within their joined activities
  - Title, question content, and upvote count
  - View all questions for an activity
  - Sort by newest, most upvoted, or unanswered

- **Answers**:
  - Any member can answer questions
  - Display answerer's name and role
  - Multiple answers per question
  - Threaded discussion format

- **Engagement Features**:
  - Upvote questions (helps prioritize)
  - Mark best answer (by question asker or admin)
  - Edit own questions/answers

### Benefits

- Fosters community interaction
- Knowledge sharing among members
- Reduces repeated questions to admins

### Database Changes

Add tables:
- `questions`: question_id, activity_id, user_id, title, content, upvotes, created_at
- `answers`: answer_id, question_id, user_id, content, created_at

---

## Issue 5: Create Personalized Dashboard & Calendar

**Labels:** `enhancement`, `ui/ux`, `medium-priority`

### Description

Build a personalized dashboard showing user's activities, upcoming events, and recent announcements.

### Proposed Features

- **Dashboard Components**:
  - "My Activities" section showing joined activities
  - Upcoming events calendar with visual display
  - Recent announcements feed
  - Quick stats (total activities, pending requests)

- **Calendar Integration**:
  - Display activity schedules on calendar
  - Event dates from announcements
  - Color-coded by activity
  - Month/week/day views

- **Navigation**:
  - Click activity to see details
  - Click event to see full announcement
  - Filter by activity

### Benefits

- Better user engagement
- Quick access to relevant information
- Visual schedule management

### Technical Notes

- Use React Calendar or FullCalendar library
- Responsive design for mobile
- AJAX updates without page reload

---

## Issue 6: Add Club Administration Tools

**Labels:** `enhancement`, `admin`, `high-priority`

### Description

Create comprehensive admin tools for club admins to manage their activities effectively.

### Proposed Features

- **Admin Dashboard** showing:
  - Total member count
  - Pending requests count
  - Recent activity statistics

- **Member Management**:
  - View all current members
  - Remove members with confirmation
  - Export member list

- **Request Queue**:
  - View all pending requests
  - Bulk approve/reject
  - Sort by request date
  - Quick view applicant profiles

- **Activity Management**:
  - Edit activity details (description, schedule, capacity)
  - Upload activity images
  - Archive/unarchive activities
  - View activity history

### Access Control

- Only accessible by CLUB_ADMIN and SUPER_ADMIN roles
- Club admins see only their activities
- Super admins see all activities

---

## Issue 7: Migrate to MySQL Database

**Labels:** `enhancement`, `infrastructure`, `high-priority`, `breaking-change`

### Description

Replace in-memory storage with MySQL database for data persistence and scalability.

### Proposed Features

- **Database Schema** with tables:
  - users
  - activities
  - user_activities (join table)
  - club_requests
  - announcements
  - questions
  - answers

- **ORM Integration**:
  - Use SQLAlchemy for Python ORM
  - Define models for all entities
  - Relationship mappings

- **Migration System**:
  - Alembic for database migrations
  - Seed data script for initial activities
  - Data validation at database level

### Benefits

- Data persists across server restarts
- Better query performance
- Support for concurrent users
- Enable advanced features (search, analytics)

### Technical Requirements

- MySQL 8.0+ or MariaDB
- SQLAlchemy ORM
- Alembic for migrations
- Database connection pooling
- Environment-based configuration

---

## Issue 8: Enhance UI/UX with Modern Framework

**Labels:** `enhancement`, `frontend`, `medium-priority`

### Description

Upgrade frontend to modern framework (React) with improved UI/UX, state management, and responsive design.

### Proposed Features

- **React Frontend**:
  - Component-based architecture
  - Redux for state management
  - React Router for navigation
  - Reusable components

- **UI Improvements**:
  - Search and filter activities
  - Activity images/logos
  - Better mobile responsiveness
  - Loading states and spinners
  - Error boundaries

- **UX Enhancements**:
  - Toast notifications
  - Confirmation dialogs
  - Form validation feedback
  - Smooth transitions and animations

- **Design System**:
  - Consistent color scheme
  - Typography system
  - Spacing and layout grid
  - Accessible components (WCAG 2.1)

### Technical Stack

- React 18+
- Redux Toolkit
- React Router v6
- CSS Modules or Styled Components
- React Icons

---

## Issue 9: Add Swagger/OpenAPI Documentation

**Labels:** `enhancement`, `documentation`, `low-priority`

### Description

Implement Swagger/OpenAPI documentation for all API endpoints to improve developer experience.

### Proposed Features

- **API Documentation**:
  - Auto-generated from code annotations
  - Interactive testing interface
  - Request/response examples
  - Authentication documentation

- **Documentation Content**:
  - All endpoints with descriptions
  - Request parameters and body schemas
  - Response status codes
  - Error response formats
  - Authentication flows

- **Integration**:
  - Available at `/docs` endpoint
  - Swagger UI interface
  - Export OpenAPI spec

### Benefits

- Easier for developers to understand API
- Interactive testing without Postman
- Auto-updated documentation
- Clear API contracts

### Technical Requirements

- FastAPI's built-in OpenAPI support (already included!)
- Add detailed docstrings to endpoints
- Define Pydantic models for request/response
- Add examples and descriptions

---

## Issue 10: Implement Image Upload for Activities

**Labels:** `enhancement`, `media`, `low-priority`

### Description

Allow admins to upload and display images/logos for activities to make them more visually appealing.

### Proposed Features

- **Image Upload**:
  - Upload during activity creation
  - Update existing activity images
  - Support common formats (JPG, PNG, GIF)
  - Image validation and size limits

- **Image Storage**:
  - Store as BLOB in database OR
  - Save to file system with path in database OR
  - Use cloud storage (S3, Cloudinary)

- **Image Display**:
  - Thumbnail in activity list
  - Full size in activity details
  - Default placeholder if no image
  - Lazy loading for performance

- **Image Management**:
  - Delete/replace images
  - Image optimization (resize, compress)
  - Alt text for accessibility

### Technical Considerations

- File upload handling with multipart/form-data
- Image validation (type, size, dimensions)
- Storage solution choice
- CDN for serving images (optional)
- Base64 encoding for API responses OR URL references

---

## Priority Summary

### High Priority (Start Here)
1. User Authentication & Registration System
2. Request/Approval Workflow System
3. Club Administration Tools
4. Migrate to MySQL Database

### Medium Priority (After Core Features)
5. Announcements & Events System
6. Q&A / Discussion Forum
7. Personalized Dashboard & Calendar
8. Enhanced UI/UX with React

### Low Priority (Nice to Have)
9. Swagger/OpenAPI Documentation
10. Image Upload for Activities

---

## Implementation Notes

- Start with authentication as it's foundational for other features
- Database migration should come early to support new features
- Consider implementing features in sprints of 1-2 weeks each
- Test thoroughly after each feature implementation
- Update documentation as you build

Good luck with your project! 🚀
