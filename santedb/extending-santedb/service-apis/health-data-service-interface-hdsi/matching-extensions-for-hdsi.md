# Matching Extensions for HDSI

The HDSI resource plugins provide a 

## Querying / Flagging Matches

### Get Global Flagged Candidates

GET /hdsi/Patient/$match

### Flag Global Candidate Matches

POST /hdsi/Patient/$match

### Get Candidate Matches

GET /hdsi/Patient/{uuid}/$match

### Ignore Candidate Match

DELETE /hdsi/Patient/{uuid}/$match/{uuid of match}

### Get Merged Resources

GET /hdsi/Patient/{uuid}/$merge

### Unmerge Resource

DELETE /hdsi/Patient/{uuid}/$merge/{uuid of merge}

### Merge Resource

POST /hdsi/Patient/{uuid}/$merge/{uuid of candidate}

