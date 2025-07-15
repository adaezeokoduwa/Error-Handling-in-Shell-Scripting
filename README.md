# Error-Handling-in-Shell-Scripting

## Mini Project: Error Handling in Shell Scripting

This project focused on the importance of error handling in shell scripting, highlighting its role in improving script reliability, robustness, and user experience. I learned how to identify potential sources of errors such as user input issues, system failures, and file or command problems. The project emphasized using conditional statements (if, elif, else) and checking exit status codes (`$?`) to detect and handle errors effectively. I also learned to provide informative error messages to help users understand and resolve issues. A practical example involving AWS S3 bucket creation was implemented, where the script checks for existing buckets using the `aws s3api head-bucket` command before creating new ones. This prevents redundant resource creation and provides clear feedback on script execution success or failure. The exercise demonstrated how strategic error handling can make shell scripts more efficient, predictable, and user-friendly.

## 🛠️ Implementation

Here is the actual script I wrote to create S3 buckets for different departments with proper error handling:

```
#!/bin/bash

# Function to create S3 buckets for different departments
create_s3_buckets() {
    company="datawise"
    departments=("Marketing" "Sales" "HR" "Operations" "Media")

    for department in "${departments[@]}"; do
        bucket_name="${company}-${department}-Data-Bucket"

        # Check if the bucket already exists
        if aws s3api head-bucket --bucket "$bucket_name" 2>/dev/null; then
            echo "Bucket '$bucket_name' already exists."
        else
            # Attempt to create the bucket
            aws s3api create-bucket --bucket "$bucket_name" --region us-east-1

            # Check if the creation was successful
            if [ $? -eq 0 ]; then
                echo "Bucket '$bucket_name' created successfully."
            else
                echo "Failed to create bucket '$bucket_name'."
            fi
        fi
    done
}

# Execute the function
create_s3_buckets
```
