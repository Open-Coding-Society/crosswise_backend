# CrossWise Backend

A comprehensive Flask-based backend application used for predicting and managing border crossing wait times at San Ysidro and Otay Mesa crossings, with additional features for user management, real-time data analysis, and community interaction.

## Overview

CrossWise_Backend is a sophisticated backend system used in conjunction with a frontend.
The project as a whole is designed to help users navigate border crossings more efficiently by providing:
- Real-time and predictive wait time analysis
- Traffic incident reporting
- Weather, calendar, and historical data integration
- Community features for sharing experiences
- Administrative tools for system management

## Key Features

### Core Functionality
- **Border Wait Time Predictions**: ML-powered predictions using historical data
- **Real-time Traffic Updates**: Integration with CBP (Customs and Border Protection) APIs
- **Weather Integration**: NOAA weather data for San Diego region
- **Traffic Incident Reporting**: User-submitted reports about accidents and conditions
- **Timelapse Generation**: Create timelapse videos from border camera feeds

### User Features
- **Authentication**: JWT-based authentication with role-based access control
- **Facial Recognition**: Alternative authentication method using face recognition
- **User Profiles**: Manage user information, interests, and followers
- **Community Features**: Chat channels, posts, and discussion groups

### Administrative Features
- **User Management**: Create, read, update, delete users with role assignments
- **System Health Monitoring**: CPU, RAM, disk usage monitoring
- **Data Dashboard**: Visualize historical border crossing data
- **Reports**: Generate various system and user activity reports

## Architecture

### Technology Stack
- **Framework**: Flask 
- **Database**: SQLAlchemy ORM with SQLite (dev)
- **Authentication**: JWT tokens with Flask-Login
- **ML Libraries**: scikit-learn, pandas, numpy
- **API Design**: RESTful architecture with Flask-RESTful
- **Real-time Data**: Integration with external APIs (CBP, NOAA)

### Project Structure
```
crosswise_backend/
├── api/                          # API endpoints directory
│   ├── user.py                   # User management APIs
│   │   ├── POST   /api/user                    # Create single user
│   │   ├── GET    /api/user                    # Get current user
│   │   ├── PUT    /api/user                    # Update user
│   │   ├── DELETE /api/user                    # Delete user
│   │   ├── POST   /api/users                   # Bulk create users
│   │   ├── GET    /api/users                   # Get all users
│   │   ├── POST   /api/authenticate            # Login
│   │   ├── DELETE /api/authenticate            # Logout
│   │   ├── GET    /api/id                      # Get user ID
│   │   ├── GET    /api/followers               # Get followers
│   │   ├── GET    /api/following               # Get following
│   │   └── GET    /api/mutual_connections      # Get mutual connections
│   │
│   ├── border.py                 # Border prediction APIs
│   │   └── POST   /api/border/predict          # Predict wait time
│   │
│   ├── weather_api.py            # Weather data APIs
│   │   ├── GET    /api/weather-now             # Current weather
│   │   └── GET    /api/forecast-week           # Weekly forecast
│   │
│   ├── traffic_report.py         # Traffic incident APIs
│   │   ├── POST   /api/traffic_report/submit   # Submit report
│   │   ├── GET    /api/traffic_report/recent   # Get recent reports
│   │   └── POST   /api/traffic_report/location # Get by location
│   │
│   ├── border_feedback.py        # Border feedback APIs
│   │   ├── POST   /api/border_feedback/submit  # Submit feedback
│   │   └── GET    /api/border_feedback/recent  # Get recent feedback
│   │
│   ├── contact.py                # Contact form APIs
│   │   ├── POST   /api/contact/signup          # Submit contact info
│   │   ├── GET    /api/contact/list            # Get all contacts
│   │   └── GET    /api/contact/stats           # Get contact stats
│   │
│   ├── accident.py               # Accident prediction API
│   │   └── POST   /api/accident/predict        # Predict survival
│   │
│   ├── cancer.py                 # Cancer prediction API
│   │   └── POST   /api/cancer/predict          # Predict outcome
│   │
│   ├── estonia.py                # Estonia prediction API
│   │   └── POST   /api/estonia/predict         # Predict survival
│   │
│   ├── titanic.py                # Titanic prediction API
│   │   └── POST   /api/titanic/predict         # Predict survival
│   │
│   ├── timelapse.py              # Timelapse generation APIs
│   │   ├── POST   /api/timelapse/              # Generate timelapse
│   │   ├── GET    /api/timelapse/proxy_video   # Proxy video stream
│   │   ├── GET    /api/timelapse/history       # Get stored videos
│   │   └── GET    /api/timelapse/local_video   # Get local video
│   │
│   ├── user_facial.py            # Facial recognition APIs
│   │   ├── POST   /user/facial/register        # Register face
│   │   └── POST   /user/facial/recognize       # Recognize face
│   │
│   ├── historicalgraph_api.py    # Historical data visualization
│   │   └── GET    /api/visualization           # Get visualization
│   │
│   ├── interests.py              # User interests APIs
│   │   ├── GET    /api/interests               # Get interests
│   │   ├── POST   /api/interests               # Create interests
│   │   ├── PUT    /api/interests               # Update interests
│   │   └── DELETE /api/interests               # Delete interest
│   │
│   ├── chat.py                   # Chat messaging APIs
│   │   ├── POST   /api/chat                    # Create message
│   │   ├── GET    /api/chat                    # Get messages
│   │   ├── PUT    /api/chat                    # Update message
│   │   ├── DELETE /api/chat                    # Delete message
│   │   ├── POST   /api/chats/channel           # Get by channel
│   │   └── POST   /api/chats/filter            # Filter messages
│   │
│   ├── chat_met.py               # Alternative chat APIs
│   │   ├── POST   /api/chatmet                 # Create message
│   │   ├── GET    /api/chatmet                 # Get messages
│   │   ├── PUT    /api/chatmet                 # Update message
│   │   ├── DELETE /api/chatmet                 # Delete message
│   │   ├── POST   /api/chatsmet/channel        # Get by channel
│   │   └── POST   /api/chatsmet/filter         # Filter messages
│   │
│   ├── post.py                   # Post management APIs
│   │   ├── POST   /api/post                    # Create post
│   │   ├── GET    /api/post                    # Get single post
│   │   ├── PUT    /api/post                    # Update post
│   │   ├── DELETE /api/post                    # Delete post
│   │   ├── GET    /api/post/user               # Get user's posts
│   │   ├── POST   /api/posts                   # Bulk create posts
│   │   ├── GET    /api/posts                   # Get all posts
│   │   └── POST   /api/posts/filter            # Filter posts
│   │
│   ├── post_met.py               # Alternative post APIs
│   │   ├── POST   /api/postmet                 # Create post
│   │   ├── GET    /api/postmet                 # Get single post
│   │   ├── PUT    /api/postmet                 # Update post
│   │   ├── DELETE /api/postmet                 # Delete post
│   │   ├── GET    /api/postmet/user            # Get user's posts
│   │   ├── POST   /api/postsmet                # Bulk create posts
│   │   ├── GET    /api/postsmet                # Get all posts
│   │   └── POST   /api/postsmet/filter         # Filter posts
│   │
│   ├── group.py                  # Group management APIs
│   │   ├── POST   /api/group                   # Create group
│   │   ├── GET    /api/group                   # Get single group
│   │   ├── PUT    /api/group                   # Update group
│   │   ├── DELETE /api/group                   # Delete group
│   │   ├── POST   /api/groups                  # Bulk create groups
│   │   ├── GET    /api/groups                  # Get all groups
│   │   ├── POST   /api/groups/filter           # Filter by section
│   │   └── POST   /api/group/filter            # Get by name
│   │
│   ├── section.py                # Section management APIs
│   │   ├── POST   /api/section                 # Create section
│   │   ├── GET    /api/section                 # Get single section
│   │   ├── PUT    /api/section                 # Update section
│   │   ├── DELETE /api/section                 # Delete section
│   │   ├── POST   /api/sections                # Bulk create sections
│   │   └── GET    /api/sections                # Get all sections
│   │
│   ├── channel.py                # Channel management APIs
│   │   ├── POST   /api/channel                 # Create channel
│   │   ├── GET    /api/channel                 # Get single channel
│   │   ├── PUT    /api/channel                 # Update channel
│   │   ├── DELETE /api/channel                 # Delete channel
│   │   ├── POST   /api/channels                # Bulk create channels
│   │   ├── GET    /api/channels                # Get all channels
│   │   ├── POST   /api/channels/filter         # Filter by group
│   │   └── POST   /api/channel/filter          # Get by name
│   │
│   ├── pfp.py                    # Profile picture APIs
│   │   ├── GET    /api/id/pfp                  # Get profile picture
│   │   ├── PUT    /api/id/pfp                  # Update profile picture
│   │   └── DELETE /api/id/pfp                  # Delete profile picture
│   │
│   ├── health.py                 # System health monitoring
│   │   └── GET    /api/health                  # Get system health
│   │
│   ├── usettings.py              # Application settings API
│   │   ├── GET    /api/settings                # Get settings
│   │   ├── POST   /api/settings                # Create settings
│   │   └── PUT    /api/settings                # Update settings
│   │
│   ├── user_met.py               # Alternative user APIs
│   │   ├── POST   /api/usermet                 # Create user
│   │   ├── GET    /api/usermet                 # Get current user
│   │   ├── PUT    /api/usermet                 # Update user
│   │   ├── DELETE /api/usermet                 # Delete user
│   │   ├── POST   /api/usersmet                # Bulk create users
│   │   ├── GET    /api/usersmet                # Get all users
│   │   ├── POST   /api/authenticatemet         # Login
│   │   ├── DELETE /api/authenticatemet         # Logout
│   │   ├── GET    /api/id                      # Get user ID
│   │   └── GET    /api/followersmet            # Get followers
│   │
│   ├── twitter_search.py         # Twitter integration
│   │   └── (Background task - no REST endpoints)
│   │
│   └── jwt_authorize.py          # JWT authentication decorator
│
├── model/                        # Database models & ML models
│   ├── user.py                   # User database model
│   ├── border.py                 # Border wait time ML model
│   ├── weather_formater.py       # Weather data processor
│   ├── traffic_report.py         # Traffic report model
│   ├── border_feedback.py        # Border feedback model
│   ├── accident.py               # Accident prediction ML model
│   ├── cancer.py                 # Cancer prediction ML model
│   ├── estonia.py                # Estonia prediction ML model
│   ├── titanic.py                # Titanic prediction ML model
│   ├── timelapse.py              # Timelapse generation model
│   ├── facial_encoding.py        # Facial recognition model
│   ├── twitter.py                # Twitter data model
│   ├── post.py                   # Post database model
│   ├── chat.py                   # Chat database model
│   ├── group.py                  # Group database model
│   ├── section.py                # Section database model
│   ├── channel.py                # Channel database model
│   ├── vote.py                   # Vote database model
│   ├── poll.py                   # Poll database model
│   ├── language.py               # Language database model
│   ├── player.py                 # Player database model
│   ├── school_classes.py         # School classes model
│   ├── help_request.py           # Help request model
│   ├── feedback.py               # Feedback model
│   ├── likes.py                  # Likes model
│   ├── topusers.py               # Top users model
│   ├── usettings.py              # Settings model
│   ├── pfp.py                    # Profile picture utilities
│   ├── calendar_dataprocessing.py # Calendar data processor
│   └── calendarscore.py          # Calendar event scoring
│
├── templates/                    # HTML templates
│   ├── layouts/
│   │   ├── base.html            # Base template
│   │   ├── navbar.html          # Navigation bar
│   │   └── project.html         # Project layout
│   ├── index.html               # Admin dashboard
│   ├── user_index.html          # User dashboard
│   ├── login.html               # Login page
│   ├── utable.html              # User table
│   ├── u2table.html             # Alternative user table
│   ├── data_dashboard.html      # Data visualization
│   ├── ureports.html            # Reports page
│   ├── usettings.html           # Settings page
│   ├── uhealth.html             # System health
│   ├── uhelp.html               # Help requests
│   ├── ugeneralsettings.html   # General settings
│   ├── uabout.html              # About page
│   ├── uvote.html               # Vote management
│   ├── chatData.html            # Chat data
│   ├── postData.html            # Post data
│   ├── languageData.html        # Language data
│   ├── pollData.html            # Poll data
│   ├── 404.html                 # 404 error page
│   └── unauthorized.html        # Unauthorized page
│
├── static/                      # Static assets
│   ├── assets/                  # Images and media
│   └── js/                      # JavaScript files
│
├── scripts/                     # Utility scripts
│   ├── db_init.py              # Initialize database
│   ├── db_backup.py            # Backup database
│   ├── db_restore.py           # Restore database
│   ├── venv.sh                 # Virtual environment setup
│   └── prism_backup_sequence.sh # Backup sequence
│
├── datasets/                    # Data files
│   ├── january.json            # January wait times
│   ├── february.json           # February wait times
│   ├── march.json              # March wait times
│   ├── april.json              # April wait times
│   ├── san_diego_weather.csv   # Weather data
│   ├── estonia-passenger-list.csv
│   ├── accident.csv
│   ├── haberman.csv            # Cancer data
│   ├── calendar_parsedevents.csv
│   └── calendar_unparsedevents.csv
│
├── data/                       # Dynamic data storage
│   ├── videos/                 # Stored video files
│   ├── contacts.txt            # Contact submissions
│   └── contacts.json           # Contact data JSON
│
├── instance/                   # Instance-specific files
│   ├── volumes/                # Database files
│   └── uploads/                # User uploads
│
├── requirements.txt            # Python dependencies
├── docker-compose.yml          # Docker composition
├── Dockerfile                  # Docker image config
├── main.py                     # Application entry point
├── __init__.py                 # App initialization
├── app.py                      # Legacy Flask app
└── .env                        # Environment variables
```

## Installation

### Prerequisites
- Python 3.12+
- pip
- Virtual environment (recommended)
- Docker (optional, recommended)

### Local Development Setup

1. **Clone the repository**
```bash
git clone <repository-url>
cd crosswise_backend
```

2. **Create and activate virtual environment**
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. **Install dependencies**
```bash
pip install -r requirements.txt
```

4. **Set up environment variables**
Create a `.env` file in the project root:
```env
# Authentication
ADMIN_USER=admin
ADMIN_PASSWORD=secure-password

# External APIs
TWITTER_BEARER_TOKEN=your-twitter-token

```

5. **Initialize the database**
```bash
python scripts/db_init.py
```

6. **Run the application**
```bash
python main.py
```

The application will be available at `http://localhost:3167`

## Configuration

### Database Configuration
- **Development**: SQLite database stored in `instance/volumes/`
  
### CORS Configuration
Allowed origins:
- `http://localhost:4887`
- `https://illuminati1618.github.io`

### File Upload Settings
- Maximum file size: 5MB
- Allowed extensions: `.jpg`, `.png`, `.gif`

## API Documentation

### Authentication Endpoints

#### Login
```http
POST /api/authenticate
Content-Type: application/json

{
  "uid": "username",
  "password": "password"
}
```

#### Logout
```http
DELETE /api/authenticate
```

### Border Prediction API

#### Get Wait Time Prediction
```http
POST /api/border/predict
Content-Type: application/json

{
  "mode": "long_term",  // or "real_time"
  "day": 0,            // 0-6 (Sunday-Saturday)
  "month": "january",   
  "time": 14           // 0-23 (hour)
}
```

### User Management API

#### Create User
```http
POST /api/user
Content-Type: application/json

{
  "name": "John Doe",
  "uid": "johndoe",
  "email": "john@example.com",
  "phone": "123-456-7890"
}
```

#### Get Current User
```http
GET /api/user
Authorization: Bearer <token>
```

### Traffic Report API

#### Submit Traffic Report
```http
POST /api/traffic_report/submit
Content-Type: application/json

{
  "report_time": "2024-05-30T14:30:00",
  "reason": "accident",  // traffic, accident, natural disaster, etc.
  "border_location": "San Ysidro",  // or "Otay Mesa"
  "direction": "entering us",  // or "entering mexico"
  "comments": "Major accident blocking 2 lanes"
}
```

### Weather API

#### Get Current Weather
```http
GET /api/weather-now
```

#### Get Weekly Forecast
```http
GET /api/forecast-week
```

## Database Models

### Core Models

#### User Model
- **Fields**: id, name, uid, email, phone, password, role, profile_picture, followers
- **Relationships**: posts, moderated_groups
- **Features**: Password hashing, JWT token generation, role-based access

#### BorderWaitTime Model
- **Purpose**: Stores and predicts border crossing wait times
- **ML Features**: Random Forest and Decision Tree models
- **Data**: Historical wait time data by day, time slot, and month

#### TrafficReport Model
- **Fields**: report_time, reason, border_location, direction, comments
- **Purpose**: User-submitted traffic incident reports

#### BorderFeedback Model
- **Fields**: time_cross, time_taken, time_diff, user_message
- **Purpose**: User feedback on actual vs predicted wait times

### Social Features Models

#### Post Model
- **Fields**: title, comment, content, user_id, channel_id
- **Relationships**: belongs to user and channel

#### Chat Model
- **Fields**: message, user_id, channel_id
- **Purpose**: Real-time messaging within channels

#### Group/Channel Models
- **Structure**: Sections → Groups → Channels → Posts/Chats
- **Purpose**: Organize community discussions

## Machine Learning Models

### Border Wait Time Prediction
- **Models**: Random Forest Regressor, Decision Tree Regressor
- **Features**: day of week, time slot, month
- **Training Data**: Historical CBP wait time data

## Development

### Backup and Restore
```bash
# Backup database
python scripts/db_backup.py

# Restore database
python scripts/db_restore.py
```

## Deployment

### Docker Deployment
```bash
# Build image
docker build -t crosswise .

# Run with docker-compose
docker-compose up -d
```

### Nginx Configuration
```nginx
server {
    listen 80;
    server_name crosswise.stu.nighthawkcodingsociety.com;
    
    location / {
        proxy_pass http://localhost:3167;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

## Additional Features

### Timelapse Generation
- Fetches videos from border cameras
- Creates timelapse videos using moviepy
- Accessible via `/api/timelapse`

### Facial Recognition
- Alternative authentication method
- Uses face_recognition library
- Endpoints: `/user/facial/register` and `/user/facial/recognize`

### Calendar Integration
- Event impact analysis on border traffic
- Processes CSV files with San Diego events
- Predicts traffic levels based on events

### System Health Monitoring
- Real-time system metrics
- CPU, RAM, disk usage tracking
- Network interface monitoring
- Available at `/api/health`

## Contributing

Use this as inspiration, NOT A PROJECT!

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request
