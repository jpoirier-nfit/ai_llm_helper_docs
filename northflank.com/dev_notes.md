# Dev added notes

**AI Processing Notes for Helm Chart Conversion:**

## Templates

- NEVER LEAVE COMMENTS IN TEMPLATES. THE JSON WILL BREAK
- When setting `name` you must follow `/^[a-zA-Z0-9]+((-|\s)[a-zA-Z0-9]+)*$/`

### Volume Spec Definition

**Only these fields are allowed for a Volume type:**

```json
{
	"kind": "Volume",
	"spec": {
		"spec": {
			"storageSize": 1024,
			"storageClassName": "standard"
		},
		"mounts": [
			{
				"containerMountPath": "/data"
			}
		],
		"name": "my-volume",
		"attachedObjects": [
			{
				"id": "${refs.some-service.id}",
				"type": "service"
			}
		],
		"tags": []
	},
	"ref": "my-volume-ref"
}
```

**Any other fields should be omitted or flagged as invalid.**

### Deployment Service Definition

**Only these fields are allowed for a DeploymentService type:**

```json
{
	"kind": "DeploymentService",
	"spec": {
		"name": "my-deployment-service",
		"projectId": "my-project",
		"infrastructure": {
			"architecture": "x86"
		},
		"billing": {
			"deploymentPlan": "standard-2gb"
		},
		"deployment": {
			"type": "deployment",
			"instances": 1,
			"internal": {
				"id": "build-123",
				"branch": "main",
				"buildSHA": "abc123def456",
				"buildId": "build-xyz"
			},
			"metadata": {
				"labels": {},
				"annotations": {}
			}
		},
		"loadBalancing": {
			"mode": "leastConnection"
		},
		"ports": [
			{
				"name": "http",
				"internalPort": 8080,
				"protocol": "HTTP",
				"security": {
					"credentials": [
						{
							"username": "user",
							"type": "basic-auth"
						}
					],
					"verificationMode": "or"
				},
				"public": true
			},
			{
				"name": "https",
				"internalPort": 443,
				"protocol": "HTTP",
				"security": {
					"sso": {
						"organizationId": "org_123456",
						"directoryGroupIds": ["directory_group_7890"],
						"validateInternalTraffic": true,
						"allowInternalTrafficViaPublicDns": false
					},
					"verificationMode": "or"
				},
				"domains": ["example.com/app", "example.com/static"],
				"disableNfDomain": true,
				"public": true
			}
		]
	}
}
```

**Any other fields should be omitted or flagged as invalid.**
