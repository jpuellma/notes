import boto3

# Create an IAM client
iam = boto3.client('iam')

def list_role_policy_attachments():
    roles = iam.list_roles()['Roles']
    report = []

    # Iterate over each role
    for role in roles:
        role_name = role['RoleName']
        role_arn = role['Arn']
        print(f"Processing role: {role_name}")
        
        # Get managed policies attached to the role
        managed_policies = iam.list_attached_role_policies(RoleName=role_name)['AttachedPolicies']

        # Get inline policies attached to the role
        inline_policies = iam.list_role_policies(RoleName=role_name)['PolicyNames']

        # Add the role details to the report
        report.append({
            'RoleName': role_name,
            'RoleArn': role_arn,
            'ManagedPolicies': [policy['PolicyArn'] for policy in managed_policies],
            'InlinePolicies': inline_policies
        })

    return report

def generate_report():
    report = list_role_policy_attachments()

    # Print the report in a structured way
    for role in report:
        print(f"Role Name: {role['RoleName']}")
        print(f"Role ARN: {role['RoleArn']}")
        
        # Print managed policies
        print("  Managed Policies:")
        for policy in role['ManagedPolicies']:
            print(f"    - {policy}")
        
        # Print inline policies
        if role['InlinePolicies']:
            print("  Inline Policies:")
            for policy in role['InlinePolicies']:
                print(f"    - {policy}")
        else:
            print("  Inline Policies: None")
        print("-" * 40)

if __name__ == "__main__":
    generate_report()
