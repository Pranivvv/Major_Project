# AlumniConnect Project Setup Guide

This guide will help you set up and run the AlumniConnect project, which consists of a React Native mobile app, a web application, and a backend API.

## Prerequisites

Before you begin, ensure you have the following installed:

1. **Node.js** (version 18 or higher)
2. **MongoDB** (for database)
3. **Android Studio** (for Android development)
4. **Xcode** (for iOS development, macOS only)
5. **Git**

## Project Structure

The project consists of three main components:
- `AlumniConnectApp/` - React Native mobile application
- `AlumniConnectWeb/` - Web application
- `AlumniConnectApi/` - Express.js backend API

## Setting up the Mobile App (AlumniConnectApp)

1. **Install Dependencies**
   ```bash
   cd AlumniConnectApp
   npm install
   ```

2. **iOS Setup** (macOS only)
   ```bash
   cd ios
   pod install
   cd ..
   ```

3. **Configure Environment**
   - Make sure the backend API is running
   - Update the API URL in the app if needed (default is http://localhost:3000)

4. **Start the Metro Bundler**
   ```bash
   npm start
   ```
   - This will start the Metro bundler in a new terminal
   - Keep this terminal running

5. **Run the App**
   - For Android:
     ```bash
     # In a new terminal
     npm run android
     ```
     - Make sure you have an Android emulator running or a physical device connected
     - The app will be installed and launched automatically
   
   - For iOS (macOS only):
     ```bash
     # In a new terminal
     npm run ios
     ```
     - Make sure you have Xcode installed
     - The app will be installed in the iOS simulator

6. **Development Tips**
   - Press 'r' in the Metro bundler terminal to reload the app
   - Press 'd' to open developer menu
   - Use React Native Debugger for debugging
   - Check the console for any errors

## Setting up the Backend API (AlumniConnectApi)

1. **Install Dependencies**
   ```bash
   cd AlumniConnectApi
   npm install
   ```

2. **Configure Environment Variables**
   - The project includes a `dummyenv` file in the API folder
   - Copy the dummy environment file to create your `.env`:
     ```bash
     cp dummyenv .env
     ```
   - The `dummyenv` file contains all required environment variables with example values
   - Replace the example values with your actual configuration values
   - Never commit the `.env` file to version control

3. **Seed Teacher Data**
   - Import the Postman collection to add initial teacher data:
     - Open Postman
     - Click "Import" button
     - Select `alumni_connect.postman_collection.json` from the project
   - The collection contains requests to populate the database with teacher information
   - Run the requests in sequence to add the teacher data
   - Make sure your API server is running before executing the requests
   - Note: All seeded users will have "password" as their default password
   - Users should change their password after first login
   - To add student data from `studrecord.json`:
     - Login with the user having moodleId: 10000000
     - Use this account to upload and process the student records
     - The student data will be automatically processed and added to the database

4. **Start the API Server**
   ```bash
   # Development mode
   npm run dev
   
   # Production mode
   npm start
   ```

## Setting up the Web Application (AlumniConnectWeb)

1. **Install Dependencies**
   ```bash
   cd AlumniConnectWeb
   npm install
   ```

2. **Configure Environment**
   - Make sure the backend API is running
   - Update the API URL in the app if needed (default is http://localhost:3000)

3. **Start the Development Server**
   ```bash
   npm run dev
   ```
   - This will start the development server
   - The web app will be available at http://localhost:5173
   - The page will automatically reload when you make changes

4. **Build for Production**
   ```bash
   npm run build
   ```
   - This will create a production build in the `dist` directory
   - The build can be deployed to any static web server

5. **Development Tips**
   - Use the browser's developer tools for debugging
   - Check the console for any errors
   - The app uses Vite for fast development and building

## Development Workflow

1. **Mobile App Development**
   - The app uses React Native with TypeScript
   - Main entry point: `AlumniConnectApp/App.tsx`
   - Use `npm run lint` to check code quality
   - Use `npm test` to run tests

2. **API Development**
   - The backend uses Express.js with TypeScript
   - API routes are defined in the `routes` directory
   - Models are defined in the `models` directory
   - Controllers are defined in the `controllers` directory
   - Use Postman or similar tools to test API endpoints

## Troubleshooting

### Common Issues

1. **Metro Bundler Issues**
   - Clear Metro cache: `npm start -- --reset-cache`
   - Ensure all dependencies are installed correctly

2. **Build Issues**
   - Clean and rebuild the project
   - For Android: `cd android && ./gradlew clean`
   - For iOS: Clean build folder in Xcode

3. **API Connection Issues**
   - Verify the API server is running
   - Check MongoDB connection
   - Verify API endpoint URLs in the mobile app
   - Check environment variables are properly set

## Additional Resources

- React Native Documentation: https://reactnative.dev/docs/getting-started
- Express.js Documentation: https://expressjs.com/
- MongoDB Documentation: https://docs.mongodb.com/

## Support

If you encounter any issues during setup, please:
1. Check the troubleshooting section
2. Review the documentation
3. Create an issue in the project repository

Happy coding! 