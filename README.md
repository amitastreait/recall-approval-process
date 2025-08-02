# Recall Flow Approval Process

A Lightning Web Component (LWC) for recalling approval submissions directly from Approval Work Item record pages in Salesforce.

## 📋 Overview

This component allows users to recall approval processes by providing a user-friendly interface on Approval Work Item record pages. It automatically retrieves the approval submission ID and uses Salesforce REST API to recall the approval with proper error handling and user feedback.

## ✨ Features

- **One-click recall** from Approval Work Item pages
- **Automatic ID resolution** - gets approval submission ID from work item
- **Rich validation** with real-time feedback
- **Modern UI** using Lightning Design System
- **Toast notifications** for success/error feedback
- **Loading states** for better UX
- **Mobile responsive** design

## 🚀 Deployment

### Step 1: Deploy Apex Classes

Deploy the following Apex classes to your org:

```bash
# Using SFDX CLI
sf project deploy start --metadata ApexClass --target-org your_org --wait 10
```

**Files to deploy:**
- `RecallApprovalSubmissionController.cls`
- `RecallApprovalSubmissionControllerTest.cls`
- `CustomHttpMock.cls`
- `MockHttpResponseGenerator.cls`

### Step 2: Deploy VF Page (Required for Session ID)

Create a Visualforce page named `Session_Id`:

```xml
<apex:page showHeader="false" sidebar="false" cache="false">
    Start_Of_Session_Id{!$Api.Session_Id}End_Of_Session_Id
</apex:page>
```

### Step 3: Deploy Lightning Web Component

Deploy the LWC component files:

```bash
# Using SFDX CLI
sf project deploy start --metadata LightningComponentBundle --target-org your_org --wait 10
```

**Files to deploy:**
- `recallApproval.html`
- `recallApproval.js`
- `recallApproval.js-meta.xml`
- `recallApproval.css`
- `recallApproval.svg` 

### Step 4: Assign Permissions

1. **Profile/Permission Set Assignment:**
   - Add **Apex Class Access** for `RecallApprovalSubmissionController`
   - Ensure users have **API Enabled** permission

2. **Object Permissions:**
   - Read access to `Approval Work Item` object

## ⚙️ Configuration

### Step 1: Add Component to Record Page

1. **Edit Lightning Record Page:**
   - Open a `Approval Work Item` record detail page
   - Click on gear icon
   - Click **Edit Page**

2. **Add Component:**
   - From the Custom Components section, drag **Recall Approval** component
   - When asked a record Id type `{recordId}`
   - <img width="817" height="503" alt="image" src="https://github.com/user-attachments/assets/2f445155-ca39-4af1-828d-ff7447e76179" />
   - Place it in desired location (recommended: right sidebar or main content area)
   - **Save** and **Activate** the page
   - <img width="1498" height="922" alt="image" src="https://github.com/user-attachments/assets/d5650d97-307d-4fe7-9e55-ab564474d982" />

### Step 2: Component Configuration

The component automatically receives the `recordId` from the record page context. No additional configuration needed.

### Step 3: App Builder Settings

In the App Builder, you can configure:
- **Visibility Rules** (show only for pending approvals)
- **Component Properties** (if needed)

## 🎯 Usage Instructions

### For End Users

1. **Navigate to Approval Work Item:**
   - Go to any pending Approval Work Item record
   - The Recall Approval component will be visible on the page

2. **Recall Approval:**
   - Enter a **recall comment** (minimum 10 characters required)
   - Click **Recall Approval** button
   - Wait for confirmation toast message

3. **Success/Error Handling:**
   - ✅ **Success:** Green toast with confirmation message
   - ❌ **Error:** Red toast with specific error details


### Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0.0 | 2025-01-08 | Initial release |

---

## 📋 Quick Reference

### Component Files
```
force-app/main/default/
├── classes/
│   ├── RecallApprovalSubmissionController.cls
│   └── RecallApprovalSubmissionControllerTest.cls
├── lwc/recallApproval/
│   ├── recallApproval.html
│   ├── recallApproval.js
│   ├── recallApproval.js-meta.xml
│   └── recallApproval.css
└── pages/
    └── Session_Id.page
```

---

**Need additional help?** Contact your Salesforce Administrator or refer to the troubleshooting section above.
