#  Surplus - Food Waste Reduction Platform

A modern web application that connects food vendors with consumers to reduce food waste by offering surplus food at discounted prices. Surplus helps restaurants, bakeries, and cafes sell excess inventory while providing affordable, quality meals to customers.

##  Project Overview

Surplus addresses the global food waste problem by creating a marketplace where vendors can list surplus food items at reduced prices before closing time. Consumers can browse available deals, place orders, and pick up fresh food while saving money and reducing environmental impact.

**Live Demo:** [[Your Vercel URL here]](https://surplus-web-app.vercel.app/)

##  Features

### For Vendors
-  Post surplus food items with descriptions and images
-  Set original and discounted prices
-  View and manage posted items
-  Track incoming orders
-  Specify pickup time windows

### For Consumers
-  Browse available food deals near you
-  View vendor locations and details
-  Place orders instantly
-  Track order history
-  See savings on each purchase

### General
-  Secure authentication system
-  Location-based filtering
-  Real-time order management
-  Responsive design for all devices
-  Modern, intuitive UI inspired by leading food brands

##  Technologies Used

### Frontend
- **HTML5** - Semantic markup
- **CSS3** - Modern styling with gradients and animations
- **JavaScript (ES6+)** - Dynamic functionality

### Backend & Services
- **Firebase Authentication** - User management and security
- **Cloud Firestore** - NoSQL database for real-time data
- **Firebase Hosting** - Scalable hosting solution

### Deployment
- **Vercel** - Continuous deployment and hosting

##  Getting Started

### Prerequisites
- Web browser (Chrome, Firefox, Safari, Edge)
- Firebase account
- Git installed on your machine

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/your-username/surplus-app.git
cd surplus-app
```

2. **Set up Firebase**
   - Create a new Firebase project at [Firebase Console](https://console.firebase.google.com/)
   - Enable Authentication (Email/Password)
   - Create a Firestore Database
   - Copy your Firebase configuration

3. **Configure the app**
   - Open `index.html`
   - Find the Firebase configuration section (search for `firebaseConfig`)
   - Replace with your Firebase credentials:
```javascript
   const firebaseConfig = {
       apiKey: "YOUR_API_KEY",
       authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
       projectId: "YOUR_PROJECT_ID",
       storageBucket: "YOUR_PROJECT_ID.appspot.com",
       messagingSenderId: "YOUR_SENDER_ID",
       appId: "YOUR_APP_ID"
   };
```

4. **Set up Firestore Security Rules**
   
   Navigate to Firestore → Rules in Firebase Console and paste:
```javascript
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /users/{userId} {
         allow read: if true;
         allow write: if request.auth != null && request.auth.uid == userId;
       }
       
       match /foodItems/{itemId} {
         allow read: if true;
         allow create: if request.auth != null;
         allow update, delete: if request.auth != null && 
           request.auth.uid == resource.data.vendorId;
       }
       
       match /orders/{orderId} {
         allow read: if request.auth != null && 
           (request.auth.uid == resource.data.consumerId || 
            request.auth.uid == resource.data.vendorId);
         allow create: if request.auth != null;
       }
     }
   }
```

5. **Run locally**
   - Simply open `index.html` in your web browser
   - Or use a local server:
```bash
   # Using Python
   python -m http.server 8000
   
   # Using Node.js
   npx serve
```

##  Deployment

### Deploy to Vercel

1. **Install Vercel CLI** (optional)
```bash
npm i -g vercel
```

2. **Deploy**
```bash
vercel
```

Or simply:
- Push your code to GitHub
- Import the repository in [Vercel Dashboard](https://vercel.com/)
- Vercel will auto-deploy

### Deploy to Firebase Hosting
```bash
firebase init hosting
firebase deploy
```

##  Usage

### As a Vendor

1. **Sign Up** - Create a vendor account with business details
2. **Post Food** - Add surplus items with:
   - Food name and description
   - Original and discounted prices
   - Quantity available
   - Image URL
   - Pickup time window
3. **Manage Items** - View, edit, or delete your listings
4. **Track Orders** - See incoming orders from customers

### As a Consumer

1. **Sign Up** - Create a consumer account
2. **Browse Deals** - View available food items near you
3. **Place Order** - Select quantity and confirm order
4. **Pick Up** - Collect your food during the specified time window
5. **Save Money** - Enjoy quality food at discounted prices

##  Project Structure
```
surplus-app/
│
├── index.html          # Main application file
│   ├── <head>         # Meta tags, Firebase SDKs, CSS
│   ├── <body>         # HTML structure
│   │   ├── Header     # Logo, navigation, auth buttons
│   │   ├── Modals     # Login/Signup modals
│   │   ├── Home       # Guest landing page
│   │   └── Dashboards # Vendor/Consumer views
│   └── <script>       # JavaScript logic
│       ├── Firebase config
│       ├── Authentication
│       ├── Firestore operations
│       ├── UI controllers
│       └── Event handlers
│
└── README.md          # Project documentation
```

##  Design Philosophy

Surplus follows a bold, appetizing design inspired by leading food brands:
- **Color Scheme**: Red-orange gradient (#d62300 to #ff6b35)
- **Typography**: Bold, uppercase headings for impact
- **Layout**: Card-based design for easy scanning
- **Interactions**: Smooth transitions and hover effects
- **Responsive**: Mobile-first approach

##  Security

- User passwords are hashed and never stored in plain text
- Firestore security rules prevent unauthorized access
- Authentication required for all write operations
- Data validation on both client and server side
- HTTPS encryption for all data transmission

##  Environmental Impact

By connecting vendors with consumers, Surplus helps:
-  Reduce food waste sent to landfills
-  Lower carbon footprint from food production
-  Promote sustainable consumption
-  Build community awareness about food waste

##  Database Schema

### Users Collection
```javascript
{
  uid: string,
  name: string,
  email: string,
  role: "vendor" | "consumer",
  businessName: string | null,
  location: string,
  createdAt: timestamp
}
```

### Food Items Collection
```javascript
{
  id: string,
  vendorId: string,
  vendorName: string,
  vendorLocation: string,
  name: string,
  description: string,
  originalPrice: number,
  discountedPrice: number,
  quantity: number,
  image: string,
  pickupTime: string,
  status: "available" | "sold",
  createdAt: timestamp
}
```

### Orders Collection
```javascript
{
  id: string,
  consumerId: string,
  customerName: string,
  vendorId: string,
  vendorName: string,
  foodItemId: string,
  foodItemName: string,
  quantity: number,
  totalPrice: number,
  status: "pending" | "ready" | "completed",
  orderDate: timestamp
}
```

##  Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the project
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request



##  Author

**Your Name**
- GitHub: nugiYabesi [(https://github.com/nugiYabesi)]
- Email: nugiybesi@gmail.com

##  Acknowledgments

- Firebase for backend infrastructure
- Vercel for hosting platform
- Unsplash for food imagery
- Anthropic Claude for development assistance

##  Support

For support, email your.email@example.com or open an issue in the GitHub repository.

##  Future Enhancements

- [ ] Mobile app (React Native)
- [ ] Push notifications
- [ ] In-app messaging between vendors and consumers
- [ ] Rating and review system
- [ ] Analytics dashboard for vendors
- [ ] Multi-language support
- [ ] Payment gateway integration
- [ ] Google Maps integration for directions
- [ ] Loyalty rewards program
- [ ] Admin panel for platform management

---

**Made with love to reduce food waste and help communities**
