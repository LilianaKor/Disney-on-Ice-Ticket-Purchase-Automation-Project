# Disney-on-Ice-Ticket-Purchase-Automation-Project

## Project Overview

This project demonstrates an automated test scenario for purchasing tickets to the "Disney on Ice" event. The automation covers both positive and negative test cases where the number of tickets added to the cart is validated based on business rules.

The goal of this project is to showcase:

Loop-based actions (times function simulation)

Conditional branching in test flows (using "if" and "else")

Dynamic element interaction (popups, search results, buttons)

Assertion of both successful and failed conditions (positive and negative scenarios)

Modern test automation practices with Playwright

Cross-browser readiness (Chromium, Firefox, WebKit)

## Why Playwright?

Playwright is selected for this project because it aligns perfectly with the scenario requirements:

### "Times Function" Implementation:
Adding tickets multiple times is easily achieved using a for loop, mimicking the "times function" logic mentioned in the scenario.

### Dynamic Element Handling:
The scenario involves closing floating windows, verifying text presence, and interacting with dynamically appearing buttons. Playwright’s auto-waiting mechanisms ensure reliable and concise code for these steps.

### Modern Alternative to Selenium:
Playwright simplifies interactions that would require manual waits and complex handling in Selenium. It provides a robust solution with less code and greater stability, which is excellent for demonstration purposes.

### Visual Execution (headless=False):
As the scenario describes "let’s see how it works", Playwright allows running tests in visible browser mode, making it ideal for presentations and recording demo videos.

### Cross-Browser Support:
Playwright supports Chromium, Firefox, and WebKit (Safari engine), making the test ready for cross-browser validation without additional setup.

## Project Goals

Demonstrate positive and negative test cases for ticket purchasing.

Showcase proficiency in handling loops, conditions, and assertions.

Exhibit modern automation practices with Playwright.

Deliver a polished, professional automation script suitable for portfolio demonstrations.

Features

Search functionality automation.

Popup handling (floating window close).

Ticket addition using looped actions.

Error message validation for exceeding ticket limits.

Scenario-driven test execution using variables.

## How to Run

Install dependencies:
```
pip install playwright
playwright install

## Execute the test script: ```

python tests/test_ticket_purchase.py

## Test Scenarios

Positive Test Case: Add 4 tickets successfully and verify cart quantity.

Negative Test Case: Attempt to add 10 tickets and validate that an error message appears stating "You must purchase less than nine tickets."

## Repository Structure

disney_ticket_automation/
├── tests/
│   └── test_ticket_purchase.py
├── README.md
├── requirements.txt
└── allure-results/  # (optional, for Allure reporting)

## Outcome

By completing this project, I aim to demonstrate my ability to:

Design clear and structured automated tests.

Handle dynamic web interactions efficiently.

Implement positive and negative test scenarios in a maintainable way.

Present automation work that reflects real-world business workflows.

This project reflects not just a technical task but a practical approach to ensuring product quality through thoughtful automation design

##
from playwright.sync_api import sync_playwright
```

def run_test(test_type="positive"):
    with sync_playwright() as p:
        browser = p.chromium.launch(headless=False)
        page = browser.new_page()

        # Step 1: Open Website
        page.goto("https://example-ticketwebsite.com")

        # Step 2: Close Floating Window if present
        if page.is_visible("div.floating-window-close"):
            page.click("div.floating-window-close")

        # Step 3: Search for 'Disney on Ice'
        page.fill("input.search-bar", "Disney on Ice")
        page.click("button.search-button")

        # Step 4: Verify 'Frozen & Encanto' is present
        page.wait_for_selector("text=Frozen & Encanto")
        print("Found 'Frozen & Encanto'")

        # Step 5: Click on 'Find Tickets'
        page.click("text=Find Tickets")

        # Step 6: Choose 'Purchase by Price'
        page.click("text=Purchase by Price")

        # Step 7: Add Tickets
        if test_type == "positive":
            tickets_to_add = 4
        else:
            tickets_to_add = 10

        for _ in range(tickets_to_add):
            page.click("button.add-ticket")

        # Step 8: Assertions
        if test_type == "positive":
            # Assert that 4 tickets are in the cart
            cart_count = page.inner_text("span.cart-ticket-count")
            assert cart_count == "4", f"Expected 4 tickets, but found {cart_count}"
            print("Positive Test Passed: 4 tickets added.")
        else:
            # Assert error message for exceeding ticket limit
            error_message = page.inner_text("div.error-message")
            assert "must purchase less than nine tickets" in error_message
            print("Negative Test Passed: Error message displayed.")

        browser.close()

### Run Positive Test
run_test("positive")

### Run Negative Test
run_test("negative")

### Thank you for reviewing this project!

## Liliana Koretska
Automation QA Engineer | Python | Playwright | Web & Mobile Testing

