---
title: AI-Powered Travel Assistant Lab
description: Requirements for building a multimodal travel assistant with Azure AI services
author: Lab Facilitator
ms.date: 2026-08-26
ms.topic: tutorial
keywords:
  - Azure AI
  - Python
  - multimodal application
  - travel assistant
estimated_reading_time: 8
---

## Business scenario

A travel company wants to help customers plan trips more efficiently. Customers can
submit a text request, a voice note, a passport or identity document, and an image of
a destination or attraction. The application must analyze these inputs and generate a
personalized travel recommendation.

Your team will design and build a Python application that combines multiple Azure AI
services. You must determine which Azure AI service and model best fit each requirement,
explain your choices, and integrate the services into one workflow.

## Learning objectives

After completing this lab, you should be able to:

* Select suitable Azure AI services for text, speech, image, and document analysis
* Call Azure AI services from Python by using supported SDKs or REST APIs
* Combine results from multiple services into a grounded prompt
* Generate a useful itinerary with Azure OpenAI
* Handle credentials, errors, and sensitive personal data responsibly
* Present the workflow through a usable interface of your choice

## Sample user journey

A customer named Alex Morgan wants to visit Singapore with their family.

### Travel request

```text
Hi, I am planning a 5-day family trip to Singapore in December.
I have a budget of $2,000.
We enjoy theme parks, aquariums, and shopping.
```

### Voice note

```text
We are travelling with a 6-year-old child and would prefer family-friendly
attractions.
```

### Passport upload

The sample PDF contains the following fictional information:

```text
Name: Alex Morgan
Nationality: Indian
Passport Number: X123456
```

### Destination image

The image shows Universal Studios Singapore. Your solution should identify useful
visual details without assuming that every uploaded image contains the same attraction.

## Functional requirements

### Analyze the travel request

Use an Azure language analysis capability to process the request. The application must:

* Detect the input language
* Extract key phrases
* Extract named entities such as destination, date, budget, and interests
* Preserve the original request for later itinerary generation

### Process the voice note

Use an Azure speech capability to convert the voice note to text. The application must:

* Accept at least one common audio format
* Display the recognized text
* Include recognized preferences in the itinerary request
* Report an understandable error when speech cannot be recognized

### Analyze the destination image

Use an Azure vision capability to analyze the uploaded image. The application must:

* Produce a short image description or caption
* Return relevant tags or detected objects
* Include useful visual context in the itinerary request
* Avoid treating uncertain image results as verified facts

### Extract passport information

Use Azure AI Document Intelligence to extract information from the uploaded document.
The application must:

* Read a PDF or image document
* Extract the traveler's name and nationality
* Extract the passport number for demonstration purposes
* Clearly indicate fields that were not found or had low confidence

> [!WARNING]
> Use only fictional test data. Do not log, send to Azure OpenAI, or display a complete
> passport number unless it is necessary for the lab demonstration. Mask sensitive
> values in the interface and logs.

### Generate the itinerary

Use Azure OpenAI to combine the analyzed results into a personalized recommendation.
The output must include:

* A five-day, day-by-day Singapore itinerary
* Family-friendly activities suitable for a 6-year-old child
* Theme park, aquarium, and shopping recommendations
* An estimated budget breakdown that stays near the $2,000 limit
* Practical travel tips and clearly stated assumptions
* A reminder that prices, opening hours, entry rules, and visa requirements must be
  verified from authoritative sources

Do not include the passport number in the prompt sent to Azure OpenAI. Include only
document fields that are relevant to trip planning.

## Test data requirements

Create a `data/` directory for local test inputs. Include only fictional or openly
licensed content and document the source of external media.

The suggested structure is:

```text
data/
  travel-request.txt
  family-preferences.wav
  sample-passport.pdf
  singapore-attraction.jpg
  README.md
```

The `data/README.md` file must describe how each file was created, its expected content,
and any license or attribution requirements. Teams may record their own voice note and
create their own fictional passport document. Do not commit real identity documents.

## User interface

Build any usable interface, such as Streamlit, Flask, a command-line application, or a
Jupyter notebook. The interface must let a user:

* Enter or load a travel request
* Upload an audio file, identity document, and destination image
* Start the analysis
* Review intermediate results from each Azure AI service
* View the final itinerary
* Understand which step failed without losing successful results from other steps

## Technical requirements

* Use Python 3.11 or later
* Keep service endpoints, API keys, deployment names, and secrets outside source code
* Provide an example environment configuration without real secret values
* Prefer Microsoft Entra ID authentication and least-privilege access where supported
* Separate service-specific code from orchestration and interface code
* Validate file types and set reasonable upload-size limits
* Add timeouts and error handling for network calls
* Apply appropriate content-safety controls to user input and generated output
* Record latency and failures without logging prompts, passport data, or secret values
* Avoid sending raw files or unnecessary personal data to Azure OpenAI
* Include automated tests for orchestration logic by mocking Azure service responses

## Expected deliverables

Submit the following items:

* A working Python application
* A dependency manifest and setup instructions
* The fictional test data described in this lab
* An example environment configuration file
* A short architecture diagram showing services and data flow
* A service-selection table that explains each Azure AI choice
* Automated tests for the main success path and at least two failure cases
* A demonstration of the complete sample user journey

## Acceptance criteria

The lab is complete when:

1. All four input types can be supplied through the chosen interface.
2. Text analysis returns a language, key phrases, and relevant entities.
3. Speech recognition returns text that influences the recommendation.
4. Image analysis returns visual context that influences the recommendation.
5. Document processing extracts the expected fictional traveler fields.
6. Azure OpenAI produces a coherent five-day itinerary within the stated constraints.
7. Intermediate outputs and service failures are visible to the user.
8. Secrets and full passport numbers are absent from source code, prompts, and logs.
9. Setup instructions allow another participant to run the application.
10. Tests run without requiring live Azure service calls.

## Stretch goals

Teams that finish early can add one or more enhancements:

* Translate the itinerary into the detected or selected language
* Add text-to-speech playback of the final recommendation
* Ground current attraction information with Azure AI Search
* Export the itinerary as a PDF
* Add content filtering and prompt-injection defenses
* Compare latency and estimated cost across service calls

## Evaluation guidance

Evaluate solutions based on functional completeness, appropriate service selection,
quality of the generated itinerary, code organization, error handling, security and
privacy, test coverage, and clarity of the demonstration. Favor evidence that the team
understands why each service is used, not only that the happy path runs.