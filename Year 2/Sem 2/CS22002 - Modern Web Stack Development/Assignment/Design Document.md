# **1. Problem Definition**
### **Current Problem**
- Music streaming platforms like Spotify allow users to create playlists but lack **native features for collaborative group playlist creation** based on **combined listening preferences**.
- Finding friends with **similar music tastes** on Spotify is not straightforward.
- Users often have to manually create and curate group playlists, which can be time-consuming.
### **Solution**
- A web application where users **sign up, link their Spotify accounts, and find friends**.
- Users can **create group playlists**, which will be generated based on their collective music tastes.
- Users can **search for friends manually** and also see **mutual friends for easy connection**.
- Admins will have a **separate interface to manage users**.
---
# **2. Technology Stack**

|**Component**|**Technology**|**Justification**|
|---|---|---|
|**Frontend**|React OR Vanilla JS + HTML|React provides reusable components, but Vanilla JS may offer simplicity|
|**Backend**|Flask|Lightweight, integrates well with APIs, and supports Python's data processing capabilities|
|**Database**|MySQL or MongoDB|SQL for structured data (users, playlists) or NoSQL for flexibility (playlist structures, preferences)|
|**Authentication**|Spotify OAuth + Email/Password|Provides seamless Spotify login while supporting traditional authentication|
|**External APIs**|Spotify API|Retrieves user playlists, liked songs, and enables playlist creation|
|**Security**|bcrypt for password hashing, JWT for authentication|Ensures secure login and user data protection|
|**Hosting**|AWS/GCP/Heroku (for backend) + Netlify/Vercel (for frontend)|Scalable deployment options|

---
# **3. High-Level System Architecture**
### **System Flow**
1. **User Registration/Login**
    - Users sign up with **email/password** or **Spotify OAuth**.
2. **Spotify Account Linking**
    - OAuth integration retrieves **user playlists, liked songs, and top tracks**.
3. **Finding Friends**
    - Users can **search for friends manually**.
    - Mutual friends are suggested based on **existing connections**.
4. **Group Playlist Creation**
    - Users select **a theme or genre**.
    - Songs are **extracted from members’ listening history or playlists**.
    - The playlist is **saved within the app** and optionally **synced to Spotify**.
5. **Admin Controls**
    - Admins can **add/delete users** via a separate admin interface.
---
# **4. API Design**
### **Endpoints**

|Method|Endpoint|Description|Authentication|
|---|---|---|---|
|`POST`|`/api/auth/signup`|Register a new user|❌ (public)|
|`POST`|`/api/auth/login`|Login a user|❌ (public)|
|`GET`|`/api/user/profile`|Fetch user profile|✅ (JWT)|
|`POST`|`/api/user/link-spotify`|Connect Spotify account|✅ (JWT + OAuth)|
|`GET`|`/api/user/friends`|Fetch friend list|✅ (JWT)|
|`POST`|`/api/user/add-friend`|Add a new friend|✅ (JWT)|
|`GET`|`/api/playlist/generate`|Generate a group playlist|✅ (JWT + OAuth)|
|`POST`|`/api/playlist/save`|Save playlist to Spotify|✅ (JWT + OAuth)|
|`DELETE`|`/api/admin/remove-user/:id`|Admin removes a user|✅ (Admin JWT)|

### **Data Formats**
- **User Profile** (`GET /api/user/profile`)
```json
{
  "id": "12345",
  "name": "John Doe",
  "email": "johndoe@email.com",
  "spotify_connected": true,
  "friends": ["67890", "54321"]
}
```
- **Generated Playlist** (`GET /api/playlist/generate`)
```json
{
  "playlist_name": "Chill Vibes",
  "tracks": [
    {"title": "Song A", "artist": "Artist X"},
    {"title": "Song B", "artist": "Artist Y"}
  ]
}
```
---
# **5. Wireframes**
- **Client App:** User dashboard, friend search, group playlist creation.
- **Admin App:** User management interface.

---
# **6. External API Integration**
- **Spotify API**: OAuth login, fetching user’s top tracks, liked songs, and creating playlists.
- **Spotify Rate Limits**: Implement caching or batch requests to reduce API calls.
---
# **7. Security Considerations**
- **Authentication**:
    - Use **JWT tokens** for session management.
    - Encrypt passwords using **bcrypt**.
- **Data Protection**:
    - Ensure **GDPR compliance** (e.g., allow users to delete data).
    - Store **minimal sensitive user data**.
- **Prevent Abuse**:
    - Rate-limit API requests to prevent spam.
    - Require **mutual confirmation** before adding friends.
---
# **8. Legal, Ethical, and Social Issues**

### **Legal**
- **Spotify Terms of Service**: Ensure that **playlist creation adheres** to Spotify API policies.
- **GDPR Compliance**: Allow users to **delete their accounts and request data removal**.
### **Ethical**
- **User Consent**: Users must agree to **Spotify data access** before connecting accounts.
- **Avoid Misuse**: Admins should **only remove users violating policies**.
### **Social**
- **Community Building**: The app fosters **music-based social connections**.
- **Data Sharing Transparency**: Users should know **what data is stored** and why.
