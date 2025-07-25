# Dev added notes

**AI Processing Notes for Helm Chart Conversion:**

## Templates

- When generating Northflank templates, infrastructure-as-code JSON, or any config intended for Northflank, never include comments, explanations, or non-spec fields inside the code block.
- All explanations, notes, or context must be provided outside the code block.
- The code block must contain only valid Northflank JSON as defined by documentation and dev notes.
- No inline comments (//, /_ ... _/, #, or <!-- ... -->) are allowed.
- No extra fields for human readability or documentation inside the template.
- If you need to clarify or annotate, do so before or after the code block in your response.
- When setting `name` you must follow `/^[a-zA-Z0-9]+((-|\s)[a-zA-Z0-9]+)*$/`

### Addon Spec Definition

**Only these fields are allowed for an Addon type:**

```json
{
	"kind": "Addon",
	"ref": "my-addon-ref",
	"spec": {
		"type": "addon-type",
		"version": "7.4.2",
		"billing": {
			"replicas": 1,
			"storage": 4096,
			"storageClass": "standard",
			"deploymentPlan": "standard-2gb"
		},
		"tlsEnabled": true,
		"name": "my-addon"
	}
}
```

**Note:**

- Minimum `billing.storage` is 4096.
- Any other fields should be omitted or flagged as invalid.

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
