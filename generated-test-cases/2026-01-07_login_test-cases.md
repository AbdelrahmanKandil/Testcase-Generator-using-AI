# Test Cases: Login Feature

**Generated:** 2026-01-07
**Source:** feature-requirements/login.md
**Author:** Copilot

## Summary
- Total: 15
- Positive: 4
- Negative: 7
- Edge Cases: 4

## Test Cases

| # | Title | Preconditions | Steps | Expected Result | Priority |
|---|-------|---------------|-------|-----------------|----------|
| 1 | Login with valid credentials | 1. User is registered<br>2. Account is not locked | 1. Navigate to login page<br>2. Enter valid email<br>3. Enter valid password<br>4. Click Login button | User is redirected to dashboard | High |
| 2 | Login with Remember Me checked | 1. User is registered<br>2. Account is not locked | 1. Navigate to login page<br>2. Enter valid credentials<br>3. Check "Remember Me" checkbox<br>4. Click Login button | User is logged in and session persists for 30 days | Medium |
| 3 | Login with Remember Me unchecked | 1. User is registered<br>2. Account is not locked | 1. Navigate to login page<br>2. Enter valid credentials<br>3. Leave "Remember Me" unchecked<br>4. Click Login button | User is logged in and session expires after 24 hours of inactivity | Medium |
| 4 | Toggle password visibility | 1. User is on login page | 1. Navigate to login page<br>2. Enter password<br>3. Click show/hide password toggle | Password is displayed as plain text; clicking again masks it | Low |
| 5 | Login with invalid password | 1. User is registered | 1. Navigate to login page<br>2. Enter valid email<br>3. Enter wrong password<br>4. Click Login button | Error message "Invalid email or password" displayed | High |
| 6 | Login with invalid email | 1. User is not registered | 1. Navigate to login page<br>2. Enter unregistered email<br>3. Enter any password<br>4. Click Login button | Error message "Invalid email or password" displayed | High |
| 7 | Login with invalid email format | 1. User is on login page | 1. Navigate to login page<br>2. Enter invalid email format (e.g., "test@")<br>3. Click Login button | Inline validation error for invalid email format | High |
| 8 | Login with empty email field | 1. User is on login page | 1. Navigate to login page<br>2. Leave email field empty<br>3. Enter password<br>4. Attempt to click Login button | Login button is disabled; validation error shown | High |
| 9 | Login with empty password field | 1. User is on login page | 1. Navigate to login page<br>2. Enter valid email<br>3. Leave password field empty<br>4. Attempt to click Login button | Login button is disabled; validation error shown | High |
| 10 | Login with password less than 8 characters | 1. User is on login page | 1. Navigate to login page<br>2. Enter valid email<br>3. Enter password with 7 characters<br>4. Click Login button | Validation error for minimum password length | Medium |
| 11 | Account lockout after 5 failed attempts | 1. User is registered<br>2. Account is not locked | 1. Navigate to login page<br>2. Enter valid email<br>3. Enter wrong password<br>4. Repeat steps 2-3 five times | Account is locked; message indicates 15-minute lockout | High |
| 12 | Email field maximum length (255 chars) | 1. User is on login page | 1. Navigate to login page<br>2. Enter email with exactly 255 characters<br>3. Enter valid password<br>4. Click Login button | System accepts email; authentication proceeds normally | Low |
| 13 | Email field exceeds maximum length | 1. User is on login page | 1. Navigate to login page<br>2. Attempt to enter email with 256+ characters | Input is truncated or validation error shown | Low |
| 14 | Password field maximum length (128 chars) | 1. User is on login page | 1. Navigate to login page<br>2. Enter valid email<br>3. Enter password with exactly 128 characters<br>4. Click Login button | System accepts password; authentication proceeds normally | Low |
| 15 | Rate limit exceeded (10 attempts/minute) | 1. User is on login page | 1. Navigate to login page<br>2. Submit login form 11 times within 1 minute | Rate limit error displayed; further attempts blocked temporarily | High |
