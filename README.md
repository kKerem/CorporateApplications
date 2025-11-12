# Corporate Customers

Advanced corporate customer management system for WordPress and WooCommerce. Offers special pricing, a referral system, and order management for corporate customers.

## Features

### 🎯 Corporate Customer Role
- Automatic role creation
- Role assignment with the application system
- Application approval/rejection processes from the admin panel

### 💼 Application System
- Users can apply via form
- View applications in the admin panel
- Approve/reject applications
- Specify rejection reason
- Integration with the notification system

### 💰 Special Pricing
- Define corporate prices for products
- Support for corporate discounted prices
- Set minimum order quantity
- Display corporate prices on the frontend

### 🛒 Cart and Order Management
- Check minimum cart amount
- Check minimum order quantity
- List corporate orders separately
- Special menu in My Account

### 📧 Notification Integration
- Notification when application is received
- Notification when application is approved
- Notification and reason when application is rejected
- Integration with Pepech Notification System

## Requirements

- WordPress 5.0+
- WooCommerce
- Pepech Notification System (For Notifications)

## Usage

### Admin Panel

1. **Applications Page** (`wp-admin → Corporate Applications`)
- View all applications
- Filter applications (Pending, Approved, Rejected)
- Approval/Rejection of applications

2. **Settings Page**
- Set minimum cart amount
- Information about corporate customer features

### Product Editing

On the WooCommerce product editing page:

1. **Corporate Price**: Price for corporate customers
2. **Corporate Discounted Price**: Discounted price for corporate customers
3. **Corporate Minimum Quantity**: Minimum quantity to purchase at corporate pricing

### User Application

Users can apply from the My Account page:
- Apply via the `My Account → Corporate Application` link
- Apply with your company name and owner information
- Track your application status

### Corporate Customer Features

Approved corporate customers:
- See corporate pricing on product pages
- Can purchase with a minimum quantity check
- Subject to a minimum cart amount rule
- Can view their corporate orders

## Hooks and Filters

### Action Hooks

```php
// When the application is approved
do_action('pepech_corporate_application_approved', $user_id, $application_id);

// When the application is rejected
do_action('pepech_corporate_application_rejected', $user_id, $application_id, $reason);
```

### Filter Hooks

```php
// Customize corporate price
add_filter('pepech_corporate_price', function($price, $product) {
return $price * 1.1; // Add 10% commission
}, 10, 2);

// Customize minimum quantity control
add_filter('pepech_corporate_minimum_qty', function($min_qty, $product) {
return $min_qty * 2; // Double the minimum quantity
}, 10, 2);
```

## Database Structure

The plugin creates the following table:

```sql
CREATE TABLE wp_pepech_corporate_applications ( 
id mediumint(9) NOT NULL AUTO_INCREMENT, 
user_id bigint(20) NOT NULL, 
company_name varchar(255) NOT NULL, 
owner_name varchar(255) NOT NULL, 
status varchar(50) DEFAULT 'pending', 
rejection_reason text DEFAULT NULL, 
created_at datetime DEFAULT CURRENT_TIMESTAMP, 
updated_at datetime DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP, 
PRIMARY KEY (id), 
KEY user_id (user_id), 
KEY status
);
```

## Troubleshooting

### Applications Not Approved
- Recreate WordPress roles
- Deactivate and reactivate the plugin

### Prices Not Displaying
- Ensure the user has the corporate customer role
- Ensure the corporate price is defined on the product edit screen

### Minimum Cart Amount Not Working
- Ensure the minimum amount is set in the settings
- Clear the cache

## Version History

### 1.0.0
- Initial release
- Corporate customer role
- Application system
- Custom pricing
- Cart controls
- Notification integration
