# Assignment-FitPeo-Tech-

Overall Structure

Framework: React (can be created using create-react-app or Vite)

Project Layout: Component-based architecture with mock static data passed via props

Styling: Placeholder classes used (CSS to be implemented separately)



---

🏗️ Component Breakdown

1. App.jsx

Root component

Arranges the layout with a fixed sidebar and a flexible main content area

Contains: <Sidebar />, <Header />, <DashboardMainContent />



---

2. Header.jsx

Displays top navigation bar

Includes:

Logo (Healthcare.)

Static search bar

Notification icon (using Lucide icon)

User avatar and name

“Add” (+) icon




---

3. Sidebar.jsx

Vertical navigation bar on the left

Renders links (e.g., Dashboard, History, Calendar...) using icons and labels

Data sourced from navLinks.js



---

4. DashboardMainContent.jsx

Contains all main content sections:

<DashboardOverview />

<AnatomySection />

<CalendarView />

<UpcomingSchedule />

<ActivityFeed />




---

📊 Sub-Components Inside Main Content

5. DashboardOverview.jsx

Simple section heading (“Overview”) placeholder for overview cards or stats



---

6. AnatomySection.jsx

Displays a static anatomical illustration (human body)

Shows health indicators like:

Healthy Heart (green)

Lungs (red)

Bone (orange)


Data from healthData.js



---

7. CalendarView.jsx

Static calendar section (e.g., “October 2021”)

Displays static time slots and appointment cards for:

Dentist

Physiotherapy


Data from appointments.js



---

8. UpcomingSchedule.jsx

"The Upcoming Schedule" section

Groups appointments by day (e.g., On Thursday, On Saturday)

Uses the reusable <SimpleAppointmentCard />



---

9. SimpleAppointmentCard.jsx

A reusable appointment display card

Includes a dot icon, title, and time



---

10. ActivityFeed.jsx

Displays recent activity summary (e.g., “3 appointments this week”)

Shows a static bar chart (CSS bars only, no chart library used)



---

📁 Data Files

navLinks.js

Contains label/icon pairs for sidebar links (uses Lucide icons)


appointments.js

Holds static data for:

Calendar appointment slots

Upcoming schedule days and appointment details



healthData.js

Contains health status indicators for different body parts



---

🖼️ Assets

Avatars, icons, and the anatomy image (human-body.png) are referenced as /assets/...

You’ll need to include placeholder or open-source images in the public/assets/ folder



#implementation code

// File: src/App.jsx import React from 'react'; import './styles/App.css'; import Header from './components/Header'; import Sidebar from './components/Sidebar'; import DashboardMainContent from './components/DashboardMainContent';

const App = () => { return ( <div className="app-container"> <Sidebar /> <div className="main-content"> <Header /> <DashboardMainContent /> </div> </div> ); };

export default App;

// File: src/components/Header.jsx import React from 'react'; import '../styles/Header.css'; import { Bell, Plus } from 'lucide-react';

const Header = () => (

  <header className="header">
    <div className="logo">Healthcare.</div>
    <input className="search-bar" placeholder="Search" readOnly />
    <Bell className="icon" />
    <div className="user-profile">
      <img src="/assets/avatar.png" alt="User Avatar" />
      <span>John Doe</span>
    </div>
    <Plus className="icon" />
  </header>
);export default Header;

// File: src/components/Sidebar.jsx import React from 'react'; import '../styles/Sidebar.css'; import { navLinks } from '../data/navLinks';

const Sidebar = () => (

  <aside className="sidebar">
    <h3>General</h3>
    <nav>
      <ul>
        {navLinks.map((link, idx) => (
          <li key={idx}><link.icon className="nav-icon" />{link.label}</li>
        ))}
      </ul>
    </nav>
  </aside>
);export default Sidebar;

// File: src/components/DashboardMainContent.jsx import React from 'react'; import '../styles/DashboardMainContent.css'; import DashboardOverview from './DashboardOverview'; import AnatomySection from './AnatomySection'; import CalendarView from './CalendarView'; import UpcomingSchedule from './UpcomingSchedule'; import ActivityFeed from './ActivityFeed';

const DashboardMainContent = () => (

  <main className="dashboard-main">
    <DashboardOverview />
    <AnatomySection />
    <CalendarView />
    <UpcomingSchedule />
    <ActivityFeed />
  </main>
);export default DashboardMainContent;

// File: src/components/DashboardOverview.jsx import React from 'react'; import '../styles/DashboardOverview.css';

const DashboardOverview = () => (

  <section className="dashboard-overview">
    <h2>Overview</h2>
  </section>
);export default DashboardOverview;

// File: src/components/AnatomySection.jsx import React from 'react'; import '../styles/AnatomySection.css'; import { healthIndicators } from '../data/healthData';

const AnatomySection = () => (

  <section className="anatomy-section">
    <img src="/assets/human-body.png" alt="Human Anatomy" />
    <ul className="health-indicators">
      {healthIndicators.map((indicator, index) => (
        <li key={index} className={`indicator ${indicator.status.toLowerCase()}`}>
          <span>{indicator.name}</span>
          <span>{indicator.date}</span>
        </li>
      ))}
    </ul>
  </section>
);export default AnatomySection;

// File: src/components/CalendarView.jsx import React from 'react'; import '../styles/CalendarView.css'; import { calendarAppointments } from '../data/appointments';

const CalendarView = () => (

  <section className="calendar-view">
    <h2>October 2021</h2>
    <div className="calendar-grid">
      {/* Render calendar days statically or loop if needed */}
    </div>
    <div className="appointment-details">
      {calendarAppointments.map((appt, idx) => (
        <div key={idx} className="appointment-card">
          <h4>{appt.title}</h4>
          <p>{appt.time}</p>
          <p>{appt.day}</p>
        </div>
      ))}
    </div>
  </section>
);export default CalendarView;

// File: src/components/UpcomingSchedule.jsx import React from 'react'; import '../styles/UpcomingSchedule.css'; import { upcomingSchedule } from '../data/appointments'; import SimpleAppointmentCard from './SimpleAppointmentCard';

const UpcomingSchedule = () => (

  <section className="upcoming-schedule">
    <h3>The Upcoming Schedule</h3>
    {upcomingSchedule.map((day, idx) => (
      <div key={idx} className="schedule-day">
        <h4>{day.day}</h4>
        {day.appointments.map((appt, i) => (
          <SimpleAppointmentCard key={i} {...appt} />
        ))}
      </div>
    ))}
  </section>
);export default UpcomingSchedule;

// File: src/components/ActivityFeed.jsx import React from 'react'; import '../styles/ActivityFeed.css';

const ActivityFeed = () => (

  <section className="activity-feed">
    <h3>Activity</h3>
    <p>3 appointments on this week</p>
    <div className="bar-chart">
      {[1, 2, 3, 4, 5].map((bar, i) => <div key={i} className="bar" style={{ height: `${bar * 20}px` }} />)}
    </div>
  </section>
);export default ActivityFeed;

// File: src/components/SimpleAppointmentCard.jsx import React from 'react'; import '../styles/SimpleAppointmentCard.css';

const SimpleAppointmentCard = ({ title, time }) => (

  <div className="simple-appointment-card">
    <span className="dot" />
    <div>
      <h5>{title}</h5>
      <p>{time}</p>
    </div>
  </div>
);export default SimpleAppointmentCard;

// File: src/data/navLinks.js import { LayoutDashboard, History, Calendar, ClipboardList, BarChart2, FlaskConical, MessageSquare, LifeBuoy, Settings } from 'lucide-react';

export const navLinks = [ { label: 'Dashboard', icon: LayoutDashboard }, { label: 'History', icon: History }, { label: 'Calendar', icon: Calendar }, { label: 'Appointments', icon: ClipboardList }, { label: 'Statistics', icon: BarChart2 }, { label: 'Tests', icon: FlaskConical }, { label: 'Chat', icon: MessageSquare }, { label: 'Support', icon: LifeBuoy }, { label: 'Setting', icon: Settings } ];

// File: src/data/appointments.js export const calendarAppointments = [ { title: 'Dentist', time: '09:00', day: 'Tuesday' }, { title: 'Physiotherapy Appointment', time: '11:00', day: 'Wednesday' } ];

export const upcomingSchedule = [ { day: 'On Thursday', appointments: [ { title: 'Health checkup complete', time: '12:00' }, { title: 'Ophthalmologist', time: '10:00' } ] }, { day: 'On Saturday', appointments: [ { title: 'Cardiologist', time: '09:30' } ] } ];

// File: src/data/healthData.js export const healthIndicators = [ { name: 'Healthy Heart', status: 'Healthy', date: '6/11/2021' }, { name: 'Lungs', status: 'Critical', date: '10/15/2021' }, { name: 'Teeth', status: 'Healthy', date: '10/15/2021' }, { name: 'Bone', status: 'Warning', date: '7/25/2021' } ];

