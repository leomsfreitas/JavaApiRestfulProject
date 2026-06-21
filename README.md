# REST API — Vehicle Repair System

## About the Project

A RESTful API for managing vehicle repair records, including vehicle information, the responsible mechanic, and entry/exit dates. The system implements full CRUD operations with validation, pagination, and soft deletion of records.

## Technologies

- **Java 21**
- **Spring Boot 3.5.5**
- **Spring Data JPA**
- **Spring Validation**
- **H2 Database**
- **Flyway**
- **Lombok**
- **Maven**

## API Endpoints

### POST — Register Repair
```http
POST /repairs
```
```json
{
  "entryDate": "YYYY-MM-DD",
  "exitDate": "YYYY-MM-DD",
  "mechanic": {
    "mechanicName": "string",
    "yearsOfExperience": 0
  },
  "vehicle": {
    "vehicleMake": "string",
    "vehicleModel": "string",
    "vehicleYear": "YYYY",
    "vehicleColor": "string"
  }
}
```
**Response:** `201 Created` with the full repair record.

---

### GET — List All (paginated)
```http
GET /repairs?page=0&size=10
```
**Response:** `200 OK` with a page of repairs.

---

### GET — List Active (no pagination)
```http
GET /repairs/active
```
**Response:** `200 OK` with a summary list (ID, dates, mechanic name, make and model).

---

### GET — Find by ID
```http
GET /repairs/{id}
```
**Response:** `200 OK` with full details, or `404 Not Found`.

---

### PUT — Update Repair
```http
PUT /repairs
```
```json
{
  "id": 0,
  "exitDate": "YYYY-MM-DD",
  "mechanicName": "string",
  "yearsOfExperience": 0
}
```
**Response:** `200 OK` with the updated record.

---

### DELETE — Soft Delete
```http
DELETE /repairs/{id}
```
**Response:** `204 No Content`

## Database Migrations (Flyway)

Flyway is used for database versioning. Migrations are applied automatically on startup:

| Version | Description |
|---------|-------------|
| V1 | Create `repairs` table with basic fields |
| V2 | Add `vehicle_color` column |
| V3 | Add `active` column for soft deletion |
| V4 | Seed `repairs` table with sample data |

## Credits

Project developed for the **PRW3 (Web Programming 3)** course.
