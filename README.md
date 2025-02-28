# Medical Appointment Scheduler Challenge

## Overview
Create a basic appointment scheduling system that handles doctor appointments across timezones. The system should demonstrate clean code and basic timezone management.

#### Expectation
Expected time: 2-3 hours
Deadline: 3 business days from receipt

## Core Requirements

### 1. Provider Availability
- Single provider schedule: Monday to Friday, 9 AM - 5 PM EST
- Fixed 30-minute appointment slots
- No lunch breaks or holidays needed

### 2. Appointment Management
- Book appointments
- View available slots
- Handle EST and UTC timezone conversions

## Technical Design

### Data Models

```python
from datetime import datetime
from typing import List
from dataclasses import dataclass
from enum import Enum

class AppointmentStatus(Enum):
    SCHEDULED = "scheduled"
    CANCELLED = "cancelled"

@dataclass
class Appointment:
    id: str
    patient_name: str
    start_time: datetime
    end_time: datetime
    status: AppointmentStatus
    timezone: str

class SchedulingService:
    def get_available_slots(
        self,
        date: datetime,
        timezone: str = "America/New_York"
    ) -> List[datetime]:
        """Return available 30-min slots for the given date"""
        pass

    def book_appointment(
        self,
        patient_name: str,
        start_time: datetime,
        timezone: str
    ) -> Appointment:
        """Book an appointment and return booking details"""
        pass

    def list_appointments(
        self,
        date: datetime
    ) -> List[Appointment]:
        """List all appointments for a given date"""
        pass
```

### Must Have Features
- Get available slots for a given date
- Book appointments
- Basic timezone handling (EST/UTC only)
- Prevent double booking
- Basic validation of business hours

### Storage Requirements
You may use any storage solution of your choice:
- CSV file storage (recommended for simplicity)
- In-memory storage
- Simple database storage

#### CSV Storage Example
If using CSV storage, you'll need:

1. **appointments.csv** - Stores all booked appointments
```csv
id,patient_name,start_time,end_time,status,timezone
apt_123,John Doe,2024-03-20T14:30:00Z,2024-03-20T15:00:00Z,scheduled,America/New_York
```

2. **availability.csv** - Stores provider's regular schedule
```csv
day_of_week,start_time,end_time,timezone
1,09:00,17:00,America/New_York
2,09:00,17:00,America/New_York
3,09:00,17:00,America/New_York
4,09:00,17:00,America/New_York
5,09:00,17:00,America/New_York
```

### Basic Test Case
```python
from datetime import datetime

def test_basic_booking():
    service = SchedulingService()
    appointment = service.book_appointment(
        patient_name="John Doe",
        start_time=datetime(2024, 3, 20, 14, 30),
        timezone="America/New_York"
    )
    assert appointment.status == AppointmentStatus.SCHEDULED
```

