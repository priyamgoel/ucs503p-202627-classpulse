# PulseMeter and Live Quizzes

## Purpose

PulseMeter gives teachers a quick, low-stakes way to check understanding
during a lecture. Live quizzes add scored multiple-choice questions with a
leaderboard.

## Key backend files

- `code/backend/src/routes/liveActivities.js`
- `code/backend/src/routes/pulsemeters.js`
- `code/backend/src/routes/quizzes.js`
- `code/backend/src/routes/wordCloudMutes.js`
- `code/backend/src/utils/profanityFilter.js`

## Key database tables

- `live_activities`
- `pulsemeters`
- `pulsemeter_responses`
- `word_cloud_mutes`
- `quizzes`
- `quiz_questions`
- `quiz_responses`
- `activity_question_states`

## One active activity rule

A partial unique index allows only one `ACTIVE` live activity per
classroom. The instructor must end the current activity before launching
another one.

## PulseMeter flow

1. Teacher authors a reusable PulseMeter.
2. Teacher launches it in a classroom.
3. Students submit one response each.
4. The teacher sees live totals.
5. Word-cloud responses can be filtered and muted.

## Quiz scoring

WIDE mode: `300 + 700 * f`
NARROW mode: `700 + 300 * f`
Where `f` is the fraction of the time limit remaining.

## Key web files

- `code/web/src/components/CreatePulseMeterDialog.tsx`
- `code/web/src/components/PulseMeterAuthoringView.tsx`
- `code/web/src/components/LivePulseMeterModal.tsx`
- `code/web/src/components/CreateQuizDialog.tsx`
- `code/web/src/components/QuizAuthoringView.tsx`
- `code/web/src/components/LiveQuizModal.tsx`
- `code/web/src/components/QuizResultsDialog.tsx`
- `code/web/src/components/PulseMeterResultsDialog.tsx`
- `code/web/src/components/WordCloudMuteDialog.tsx`
- `code/web/src/app/student/pulse/`
- `code/web/src/app/student/quizzes/`

## Tests

- `code/backend/test/liveActivities.test.js`
- `code/backend/test/pulsemeters.test.js`
- `code/backend/test/quizzes.test.js`
- `code/backend/test/profanityFilter.test.js`

## Attendance-pending analytics

If the attendance session for the lecture has already ended, the activity
is linked to it and the present count is the denominator. Otherwise the
activity is marked pending, and it is resolved and recalculated when the
attendance session ends.

## Word-cloud moderation

A profanity filter blocks entries on submission. A teacher can mute a
student from future word clouds for a set period. The mute belongs to the
classroom and has an expiry time.

## Reference

See section 2.3.3 (PulseMeter Live Feedback) and 2.3.4 (Live Quiz Engine)
of the final project report.
