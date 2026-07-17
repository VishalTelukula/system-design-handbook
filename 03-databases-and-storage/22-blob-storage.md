# Blob Storage

Binary Large Objects (BLOBs) include:

- Images
- Videos
- PDFs
- Documents
- Backups

Blob storage systems such as Amazon S3 are designed to store massive amounts of unstructured data.

## Typical Flow

1. Upload file
2. Blob storage returns URL
3. Store URL in database
4. Replicate to CDN
5. User downloads from CDN

Instead of storing files directly in the database, store only the file URL.

The blob storage is responsible for:

- Durability
- Replication
- Serving files

## Benefits

- Cheap storage
- High durability
- Massive scalability
- CDN integration

Amazon S3 provides **99.999999999% (11 nines)** durability.

In system design, always store media files in blob storage and keep only their URLs inside the database.
