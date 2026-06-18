# ABTS_SESATS - Back4App Schema

## Question

  -----------------------------------------------------------------------
  Column                              Type
  ----------------------------------- -----------------------------------
  objectId                            String

  stem                                String

  explanation                         String

  critique                            String

  difficulty                          String

  specialty                           String

  topic                               String

  status                              String (ai_draft, in_review,
                                      needs_revision, approved, retired)

  generatedByAI                       Boolean

  aiModel                             String

  aiPromptVersion                     String

  createdBy                           Pointer -\> \_User

  approvedBy                          Pointer -\> \_User

  approvedAt                          Date

  lastEditedBy                        Pointer -\> \_User

  lastEditedAt                        Date

  createdAt                           Date

  updatedAt                           Date
  -----------------------------------------------------------------------

## QuestionOption

  Column      Type
  ----------- ------------------------
  objectId    String
  question    Pointer -\> Question
  label       String (A,B,C,D,E,...)
  text        String
  isCorrect   Boolean
  sortOrder   Number

## QuestionMedia

  -----------------------------------------------------------------------
  Column                              Type
  ----------------------------------- -----------------------------------
  objectId                            String

  question                            Pointer -\> Question

  option                              Pointer -\> QuestionOption
                                      (optional)

  mediaType                           String (image, video)

  storageProvider                     String

  fileKey                             String

  publicUrl                           String

  caption                             String

  altText                             String

  placement                           String (before_stem, after_stem,
                                      option_inline, explanation,
                                      critique)

  sortOrder                           Number

  uploadedBy                          Pointer -\> \_User

  uploadedAt                          Date

  status                              String (draft, approved, removed)
  -----------------------------------------------------------------------

## QuestionReview

  Column       Type
  ------------ --------------------------------------------
  objectId     String
  question     Pointer -\> Question
  reviewer     Pointer -\> \_User
  decision     String (approve, request_revision, reject)
  comments     String
  reviewedAt   Date

## QuestionEditHistory

  Column             Type
  ------------------ ----------------------
  objectId           String
  question           Pointer -\> Question
  editor             Pointer -\> \_User
  editedAt           Date
  previousStatus     String
  newStatus          String
  changeSummary      String
  previousSnapshot   Object (JSON)
  newSnapshot        Object (JSON)

## UserProgress

  Column           Type
  ---------------- ----------------------------
  objectId         String
  user             Pointer -\> \_User
  question         Pointer -\> Question
  selectedOption   Pointer -\> QuestionOption
  isCorrect        Boolean
  answeredAt       Date
  timeSeconds      Number

## AIGenerationJob

  Column                   Type
  ------------------------ --------------------
  objectId                 String
  specialty                String
  topic                    String
  promptVersion            String
  model                    String
  status                   String
  generatedQuestionCount   Number
  createdBy                Pointer -\> \_User
  createdAt                Date

## Suggested Roles

-   super_admin
-   editor
-   reviewer
-   content_author
-   contributor
-   subscriber
