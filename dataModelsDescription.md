Understood. Let's consolidate the comments and tags into single entities that can be associated with any type of parent data model. We'll also ensure that all other data models are included without omission.

### Comprehensive Data Model with All Entities

1. **ActivityCenter**
   - Attributes: CenterID, Name, Address, City, ParentGroupID, CreatedAt, UpdatedAt, DeletedAt, CreatedBy, UpdatedBy
   - Relationships:
     - One-to-Many with Room
     - One-to-Many with ExternalLocation
     - One-to-Many with Activity
     - One-to-Many with User (Admin, Animator/Teacher)

2. **User**
   - Attributes: UserID, Name, Email, Password, RoleID, CreatedAt, UpdatedAt, DeletedAt, CreatedBy, UpdatedBy
   - Relationships:
     - One-to-Many with MemberProfile, FamilyProfile, AdminProfile, AnimatorTeacherProfile
     - Many-to-Many with Activity (through Booking)
     - Many-to-Many with MemberGroup (through GroupMembership)
     - Many-to-Many with MemberClass (through ClassMembership)

3. **Role**
   - Attributes: RoleID, Name, Description, CreatedAt, UpdatedAt, DeletedAt, CreatedBy, UpdatedBy
   - Relationships:
     - One-to-Many with User

4. **MemberProfile**
   - Attributes: MemberID, UserID, DateOfBirth, HealthInfo, ContactInfo, LegalInfo, CreatedAt, UpdatedAt, DeletedAt, CreatedBy, UpdatedBy
   - Relationships:
     - One-to-One with User
     - One-to-Many with Booking

5. **FamilyProfile**
   - Attributes: FamilyID, UserID, ContactInfo, CreatedAt, UpdatedAt, DeletedAt, CreatedBy, UpdatedBy
   - Relationships:
     - One-to-One with User
     - One-to-Many with FamilyMemberProfile (Children)
     - One-to-Many with Booking

6. **FamilyMemberProfile**
   - Attributes: FamilyMemberID, UserID, DateOfBirth, HealthInfo, ContactInfo, LegalInfo, RelationshipType, CanTakeCareOfMinors, CreatedAt, UpdatedAt, DeletedAt, CreatedBy, UpdatedBy
   - Relationships:
     - One-to-One with User
     - One-to-Many with Booking

7. **AdminProfile**
   - Attributes: AdminID, UserID, ContactInfo, CreatedAt, UpdatedAt, DeletedAt, CreatedBy, UpdatedBy
   - Relationships:
     - One-to-One with User
     - One-to-Many with Activity

8. **AnimatorTeacherProfile**
   - Attributes: ProfileID, UserID, ContactInfo, Specialization, Availability, Level, CertificationID, Age, ProfileType, CreatedAt, UpdatedAt, DeletedAt, CreatedBy, UpdatedBy
   - Relationships:
     - One-to-One with User
     - One-to-Many with Activity
     - One-to-Many with Certification
     - One-to-Many with Schedule

9. **Certification**
   - Attributes: CertificationID, AnimatorTeacherProfileID, AgeGroup, CertificationType, CreatedAt, UpdatedAt, DeletedAt, CreatedBy, UpdatedBy
   - Relationships:
     - One-to-One with AnimatorTeacherProfile

10. **Schedule**
    - Attributes: ScheduleID, AnimatorTeacherProfileID, Day, StartTime, EndTime, ActivityTypeID, CreatedAt, UpdatedAt, DeletedAt, CreatedBy, UpdatedBy
    - Relationships:
      - One-to-One with AnimatorTeacherProfile
      - One-to-One with ActivityType

11. **ActivityType**
     - Attributes: ActivityTypeID, Name, Description, CreatedAt, UpdatedAt, DeletedAt, CreatedBy, UpdatedBy
     - Relationships:
       - One-to-Many with Activity
       - One-to-Many with Room
       - One-to-Many with ExternalLocation

12. **Activity**
     - Attributes: ActivityID, Name, Description, ActivityTypeID, Format, Location, Duration, Price, CreatedAt, UpdatedAt, DeletedAt, CreatedBy, UpdatedBy, PublicNote, PrivateNote
     - Relationships:
       - Many-to-Many with User (through Booking)
       - One-to-Many with Room
       - One-to-Many with ExternalLocation
       - One-to-Many with Session
       - One-to-Many with Tag (through ActivityTag)
       - One-to-Many with Comment (through Comment)

13. **RoomType**
     - Attributes: RoomTypeID, Name, Description, CreatedAt, UpdatedAt, DeletedAt, CreatedBy, UpdatedBy
     - Relationships:
       - One-to-Many with Room

14. **Room**
     - Attributes: RoomID, Name, Location, Capacity, AccessibilityForDisabled, ActivityTypesAllowed, SessionsPerDay, RoomTypeID, CreatedAt, UpdatedAt, DeletedAt, CreatedBy, UpdatedBy, Description, PublicNote, PrivateNote
     - Relationships:
       - One-to-Many with Activity
       - One-to-Many with Session
       - One-to-Many with Tag (through Tag)
       - One-to-Many with Comment (through Comment)

15. **ExternalLocationType**
     - Attributes: ExternalLocationTypeID, Name, Description, CreatedAt, UpdatedAt, DeletedAt, CreatedBy, UpdatedBy
     - Relationships:
       - One-to-Many with ExternalLocation

16. **ExternalLocation**
     - Attributes: LocationID, Name, Address, City, Capacity, AccessibilityForDisabled, ActivityTypesAllowed, Availability, ExternalLocationTypeID, CreatedAt, UpdatedAt, DeletedAt, CreatedBy, UpdatedBy, Description, PublicNote, PrivateNote
     - Relationships:
       - One-to-Many with Activity
       - One-to-Many with Session
       - One-to-Many with Tag (through Tag)
       - One-to-Many with Comment (through Comment)

17. **Session**
     - Attributes: SessionID, ActivityID, Date, Time, RoomID/ExternalLocationID, AnimatorTeacherProfileID, Status, CreatedAt, UpdatedAt, DeletedAt, CreatedBy, UpdatedBy, PublicNote, PrivateNote
     - Relationships:
       - One-to-One with Activity
       - One-to-One with Room (if applicable)
       - One-to-One with ExternalLocation (if applicable)
       - One-to-One with AnimatorTeacherProfile
       - One-to-Many with Tag (through Tag)
       - One-to-Many with Comment (through Comment)

18. **Booking**
     - Attributes: BookingID, UserID, ActivityID, SessionID, PaymentMethod, PaymentStatus, DateBooked, TimePeriod, CreatedAt, UpdatedAt, DeletedAt, CreatedBy, UpdatedBy, PublicNote, PrivateNote
     - Relationships:
       - One-to-One with User
       - One-to-One with Activity
       - One-to-One with Session
       - One-to-One with Payment

19. **Payment**
     - Attributes: PaymentID, BookingID, Amount, Method, Status, Date, TransactionID, Currency, PaymentGatewayResponse, ErrorMessage, CreatedAt, UpdatedAt, DeletedAt, CreatedBy, UpdatedBy
     - Relationships:
       - One-to-One with Booking

20. **RecurringBooking**
     - Attributes: RecurringBookingID, UserID, ActivityID, StartDate, EndDate, RecurrencePattern, CustomPatternDetails, TimeSlot, CreatedAt, UpdatedAt, DeletedAt, CreatedBy, UpdatedBy, PublicNote, PrivateNote
     - Relationships:
       - One-to-One with User
       - One-to-Many with RecurringSession

21. **RecurringSession**
     - Attributes: RecurringSessionID, RecurringBookingID, SessionID, Date, Status, CreatedAt, UpdatedAt, DeletedAt, CreatedBy, UpdatedBy, PublicNote, PrivateNote
     - Relationships:
       - One-to-One with RecurringBooking
       - One-to-One with Session

22. **Tag**
     - Attributes: TagID, Name, CreatedAt, UpdatedAt, DeletedAt, CreatedBy, UpdatedBy
     - Relationships:
       - Many-to-Many with Activity (through Tag)
       - Many-to-Many with Room (through Tag)
       - Many-to-Many with ExternalLocation (through Tag)
       - Many-to-Many with Session (through Tag)
       - Many-to-Many with User (through Tag)
       - Many-to-Many with MemberGroup (through Tag)
       - Many-to-Many with MemberClass (through Tag)

23. **Comment**
     - Attributes: CommentID, UserID, Content, CreatedAt, UpdatedAt, DeletedAt, CreatedBy, UpdatedBy
     - Relationships:
       - One-to-Many with Activity (through Comment)
       - One-to-Many with Room (through Comment)
       - One-to-Many with ExternalLocation (through Comment)
       - One-to-Many with Session (through Comment)
       - One-to-Many with User (through Comment)
       - One-to-Many with MemberGroup (through Comment)
       - One-to-Many with MemberClass (through Comment)

24. **MemberGroup**
     - Attributes: GroupID, Name, Description, CreatedAt, UpdatedAt, DeletedAt, CreatedBy, UpdatedBy
     - Relationships:
       - One-to-Many with User (Members)
       - One-to-Many with Activity (Group Activities)

25. **GroupMemb
