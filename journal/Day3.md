## Day 3: Terraform Troubleshooting (state)

### Case: Remote state file accidentally deleted from backend

#### Option 1: Restoring deleted state from local backup file

```
terraform state push ./path/to/backup
```

#### Option 2: Restoring deleted state with pull & push
Run the pull command and store it in a new file, then push the file to the backend
```
terraform state pull > ./path/to/restored
terraform state push ./path/to/restored
```
