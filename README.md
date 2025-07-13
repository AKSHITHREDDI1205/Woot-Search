🚀 Woot Search App
==================

This is a dynamic and responsive static web application designed to help users effortlessly discover products on Woot.com. It offers a seamless browsing experience, allowing you to search, filter by category, and quickly access product details. Built for efficiency and ease of deployment, it's perfect for hosting on platforms like AWS S3.

✨ Features
----------

-   **Product Search:** Find exactly what you're looking for by searching keywords across product titles, subtitles, and categories.

-   **Category Browsing:** Navigate through Woot's diverse product offerings with intuitive, dynamically generated category buttons at the top.

-   **Detailed Product Views:** Each product card displays essential information including its title, the Woot site it's from, a brief description, and its price range.

-   **Interactive Hover Details:** Get more insights! Hover over any product card to reveal additional details like product condition, deal start/end dates, and original price (if applicable).

-   **"Sold Out" Indicator:** Clearly marked "SOLD OUT" badges ensure you know product availability at a glance.

-   **Recent Searches History:** Your last 5 unique search queries are automatically saved and displayed, allowing for quick re-access to your favorite searches.

-   **Fully Responsive Design:** Enjoy an optimal viewing and interaction experience on any device -- be it mobile, tablet, or desktop.

-   **Lightweight & Static:** Designed for cost-effective, high-performance, and high-availability hosting.

🛠️ Technologies Used
---------------------

-   **HTML5:** The foundational structure of the web page.

-   **CSS3:** Custom styling and responsive layouts, crafted without external frameworks for maximum control.

-   **JavaScript (ES6+):** Powers all dynamic content, handles API interactions, manages search logic, and stores recent searches locally.

-   **Woot API:** The backbone for fetching real-time product data directly from Woot.com.

-   **Amazon S3:** Utilized for robust and scalable static website hosting.

-   **Terraform:** Our Infrastructure as Code (IaC) tool of choice for automating the deployment and configuration of the S3 bucket.

🚀 Setup and Deployment with Terraform (AWS S3)
-----------------------------------------------

This section provides a step-by-step guide to deploying the Woot Search App to an Amazon S3 bucket using Terraform.

### Prerequisites

-   An AWS Account with necessary permissions (S3 bucket creation, object management, and policy management).

-   AWS CLI configured on your local machine.

-   Terraform installed.

-   Your personal Woot API Key (obtainable from [developer.woot.com](https://developer.woot.com/ "null")).

### 1\. Prepare Your Application Files

1.  Save the complete HTML code of the Woot Search App into a file named `index.html`.

2.  Save the provided `error.html` code into a file named `error.html`.

3.  **Crucial Step:** Open `index.html` and locate the `WOOT_API_KEY` constant. Replace `'YOUR_WOOT_API_KEY'` with your actual Woot API Key:

    ```
    const WOOT_API_KEY = 'YOUR_WOOT_API_KEY'; // ✨ Replace this with your actual key!

    ```

### 2\. Create Terraform Configuration Files

Create a new directory for your Terraform project. Inside this directory, you will place the following Terraform configuration files:

-   **`main.tf`**: This file defines the core AWS resources for your S3 bucket, including its name, access controls (like `public-read` ACLs and public access block settings), and the configuration for static website hosting (specifying `index.html` and `error.html`). It also includes resources to upload your `index.html` and `error.html` files to the S3 bucket.

-   **`variables.tf`**: This file declares the input variables for your Terraform configuration, such as `bucket_name`, allowing you to specify the unique name for your S3 bucket when running Terraform commands.

-   **`outputs.tf`**: This file defines output values from your Terraform deployment, typically including the `website_endpoint` URL where your application will be accessible.

-   **`providers.tf`**: (Optional, but good practice for explicit provider configuration) This file would define your AWS provider configuration, including the region.

### 3\. Deploy with Terraform

1.  Open your terminal or command prompt and navigate to your `woot-s3-terraform` directory.

2.  Initialize Terraform:

    ```
    terraform init

    ```

3.  Review the planned changes (Terraform will show you exactly what resources it will create):

    ```
    terraform plan -var="bucket_name=my-unique-woot-bucket-name" # 🔑 Replace with your chosen unique bucket name!

    ```

4.  Apply the changes to deploy your S3 bucket and configure it for static website hosting:

    ```
    terraform apply -var="bucket_name=my-unique-woot-bucket-name" # 🔑 Replace with your chosen unique bucket name!

    ```

    Type `yes` when prompted to confirm.

### 4\. Access Your Website

After the files are uploaded, Terraform will conveniently output the `website_endpoint` URL. Copy this URL from your terminal and paste it into your web browser. Your Woot Search App should now be live!

Alternatively, you can find the website endpoint in the AWS S3 console:

1.  Navigate to your S3 bucket.

2.  Click on the "Properties" tab.

3.  Scroll down to the "Static website hosting" section.

💡 Usage
--------

1.  **Browse All Deals:** Upon initial loading, the app will automatically display all current featured deals from Woot.

2.  **Smart Search:** Type keywords (e.g., "vacuum", "speaker", "tools", "electronics") into the search bar and press Enter or click "Search from Woot" to intelligently filter products.

3.  **Filter by Category:** Easily narrow down your search by clicking on any of the category buttons at the top (e.g., "TECH", "HOME", "SHIRT").

4.  **Detailed View:** Simply hover your mouse over any product card to instantly reveal additional product details like its condition, deal start/end dates, and original price.

5.  **Direct Link to Woot:** Click the prominent "Go to Woot" button on any product card to seamlessly navigate directly to that product's page on Woot.com.

6.  **Quick Access:** Your last 5 unique search queries are conveniently saved and displayed as clickable buttons below the main search bar for rapid re-access.

⚠️ Important Note on API Key Security
-------------------------------------

For a production-grade application, directly embedding your Woot API Key in client-side JavaScript (`index.html`) is **strongly discouraged**. This practice exposes your key to anyone who inspects your page's source code, creating a significant security vulnerability that could lead to unauthorized usage and potential abuse.

For enhanced security, the recommended approach is to implement a backend proxy (e.g., using AWS Lambda and API Gateway). Your backend would securely store the API key and handle all communication with the Woot API, serving the data to your frontend without ever exposing the key to the client. For the scope of this demonstration project, the current client-side approach is used for simplicity.
