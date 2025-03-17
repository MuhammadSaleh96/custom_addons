# Project Extension Module

## 2. **Prerequisites**

Ensure you have the following before proceeding:

- A working Odoo instance (Community Edition) on an AWS server.
- Administrator access to Odoo.
- SSH access to the AWS instance.
- `project_extension.zip` file (or GitHub repository link).
- Visual Studio Code or PyCharm for your development workspace.

---

## **Features Overview**

### **Project Form View Enhancements**
- New fields added:
  - `project_type`
  - `industry_type`
  - `client_priority`
  - `expected_revenue`
  - `contract_signed`
- Dynamic behavior using Python to update fields based on user input.

### **Project List View Modifications**
- Displays additional fields for better visibility:
  - `project_type`
  - `industry_type`
  - `client_priority`
  - `expected_revenue`
  - `contract_signed`

### **Custom Filters for Data Retrieval**
- **High-Priority Projects:** Filters projects where `client_priority = High`.
- **Active Contracts:** Filters projects where `contract_signed = True`.
- **Government Projects:** Filters projects where `project_type = Government`.
- **Revenue Above 100,000:** Filters projects where `expected_revenue > 100,000`.

---



5. **New Project Extension Form**
   - Go to `Home Menu` on the Top-left corner Icon
   - Select `Project` from the drop-down menu
   - Click on `New` button to create a new project
   - Fill in the custom fields
   - Check the dynamic fields behavior  
     ![Dynamic Fields](images/Screenshot%202.png)
   - Click on `Create Project`
   - Click on `Projects` on the top menu bar
   - Verify that the project list view displays the new fields under two icon buttons in the image below  
     ![Project List View](images/Screenshot%203.png)

6. **Editing Existing Project Extension Form**  
   - Go to `Project` under `Home Menu` on the Top-left corner Icon  
   - Click on the `List View` Icon and choose any of the existing projects  
     ![List View Icon](images/Screenshot%204.png)  
   - Edit in the custom fields  
   - Check the dynamic fields behavior  
     ![Dynamic Fields](images/Screenshot%205.png)  
   - Save the project after editing the required fields by clicking on the icon shown in the image below  
     ![Save Project](images/Screenshot%206.png)

7. **Custom Filters Project Extension**
   - Go to `Project` under `Home Menu` on the Top-left corner Icon
   - Click on the arrow icon in the search bar and verify custom filters are retriving projects accordantly
    ![Custom Filters](images/Screenshot%207.png)

8. **Troubleshooting**  
   - Check the Odoo logs using the terminal:  
     
     ```bash
     tail -f /var/log/odoo/odoo.log
     ```

### Conclusion
 The project_extension module enhances Odoo’s Project Management capabilities by adding necessary fields, improving the user interface, and enabling advanced filtering options