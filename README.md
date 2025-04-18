# terraform
provider "aws" {
  region = "us-east-1"
}

# IAM Group
resource "aws_iam_group" "example_group" {
  name = "teraaform example-group"
}

# IAM User
resource "aws_iam_user" "example_user" {
  name = "example-user"
}

# Add User to Group
resource "aws_iam_group_membership" "example_group_membership" {
  name = "example-membership"
  users = [aws_iam_user.example_user.name]
  group = aws_iam_group.example_group.name
}

# S3 Bucket
resource "aws_s3_bucket" "example_bucket" {
  bucket = "example-terraform-bucket-123456" # must be globally unique
  force_destroy = true
}

# EC2 Instance
resource "aws_instance" "example_instance" {
  ami           = "ami-0c55b159cbfafe1f0" # Amazon Linux 2 AMI (you may want to update this)
  instance_type = "t2.micro"

  tags = {
    Name = "example-ec2"
  }
}
