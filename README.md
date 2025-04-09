# Vue Chatbot Application

## Overview

This is a simple Vue.js-based chatbot application that demonstrates a dynamic, interactive chat interface. The chatbot allows users to select and view different chat conversations, display messages, and explore associated sources.



## Features

- **Interactive Chat List**: Users can select a chat from the list to view chat history.
- **Dynamic Chat History**: Displays the chat history for the selected chat.
- **Expandable View**: The chat view can be expanded to show a detailed conversation, including relevant sources.
- **Source Panel**: Displays sources related to the conversation, accessible by clicking the source button(not yet functioning, but can be viewed in the Expanded view).
  
## Technologies Used

- **Vue 3**: The application is built using Vue 3, leveraging its composition API for better reactivity and organization.
- **CSS**: Custom styling is used for layout and component styling.
- **JavaScript/HTML**: The main code base is written in JavaScript and HTML with Vue.js.

## Installation

1. Clone the repository:

2. Navigate to the project directory:

     cd vue-chatbot

4. Install the dependencies:

    npm install

4. Start dev server:

    npm run dev


## Development Report
I approached this project by first researching existing chatbots to understand functionality and design standards. My goal was to create something user-friendly and intuitive while aligning with industry practices. After my initial research phase, I developed a simple design and mapped out the interface and functionality.

Breaking the project into distinct components helped me create a modular, maintainable system. Each component handles specific features and interactions, communicating through props to pass necessary data. This modular approach proved especially valuable for managing the chatbot's dynamic state—particularly for tracking which chat was selected and whether it was expanded or collapsed.
    
One challenge I encountered was managing smooth data flow between parent and child components. I needed to ensure that chat selection states were preserved during user interactions across different elements. This required careful handling of props and event emissions to maintain UI consistency.

For future improvements, I'd focus on better code organization. The components should be separated more effectively based on their features and purposes to enhance maintainability and scalability. The UI design also needs refinement—specifically fixing issues where text flows behind the input box and improving text area usability.

I'd also like to complete the "source" button functionality. I originally planned for this to either open a pop-up or navigate to a side page displaying relevant sources, but time constraints prevented full implementation. This would be a priority for future development.

I would also like to address unit tests, which were overlooked due to time constraints. Adding comprehensive test coverage would ensure component reliability and make future modifications safer. Additionally, I need to fix the console warnings that currently appear during runtime. These warnings, while not breaking functionality, indicate potential issues that could cause problems as the application scales.

This project gave me valuable experience in managing dynamic state, component communication, and making practical design decisions. I'm looking forward to further refining the chatbot's functionality and user experience in upcoming iterations.
