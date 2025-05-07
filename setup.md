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

## Network Setup

1. **Find Your Local IP Address**
   ```bash
   # On Windows
   ipconfig
   # Look for IPv4 Address under your active network adapter
   
   # On macOS/Linux
   ifconfig
   # or
   ip addr
   ```

2. **Update API URL in Applications**
   - Replace `localhost` with your local IP address in:
     - Mobile App: Update API URL in environment configuration
   - Example: If your local IP is 192.168.1.100, use:
     - `http://192.168.1.100:5000` for API

3. **Ensure All Devices are on Same Network**
   - Connect all devices (PC, mobile phones) to the same WiFi network
   - Make sure your firewall allows connections on ports 5000 and 5173
   - Test connectivity by pinging your local IP from other devices

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
   - Update the API URL in the app if needed (default is `http://192.168.1.19:5000`)

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

## Database Setup

1. **Install MongoDB**
   - Download and install MongoDB Community Server from [MongoDB website](https://www.mongodb.com/try/download/community)
   - Make sure MongoDB service is running on your system

2. **Create Database**
   ```bash
   # Start MongoDB shell
   mongosh

   # Create and switch to the database
   use alumniconnect

   # Verify the database is created
   show dbs
   ```

3. **Import Collections**
   ```bash
   # Navigate to the collections directory
   cd AlumniConnectApi/MongoDb\ Collections

   # Import teachers collection
   mongoimport --db alumniconnect --collection teachers --file alumniconnect.teachers.json

   # Import students collection
   mongoimport --db alumniconnect --collection students --file alumniconnect.students.json
   ```

4. **Verify Collections**
   ```bash
   # In MongoDB shell
   use alumniconnect
   show collections
   
   # Verify data in collections
   db.teachers.count()
   db.students.count()
   ```

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


3. **Start the API Server**
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
   - Update the API URL to use your local IP address (e.g., http://192.168.1.100:5000)
   - Note: All users imported from the database will have "password" as their default password
   - Users should change their password after first login

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