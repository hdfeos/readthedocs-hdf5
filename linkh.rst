Hard Link
*********

Characteristics of a hard link:

- A hard link is made with a physical address in the file
- A hard link occurs within a single file
- When a group or dataset is created, a hard link is also created
- At least one hard link exists for every group or dataset
- A hard link and the group or dataset that is the target of the link exist together (hard links cannot dangle)
- A hard link is created using H5Lcreate_hard
- A group or dataset may be the target of more than one hard link
- If a group or dataset is not the target of at least one hard link, then the group or dataset cannot be accessed, and the space occupied by the group or dataset will be reclaimed the next time the h5repack tool is run
- The target of a hard link will increase its reference count by one when the hard link is created, and the reference count will decline by one when the hard link is deleted
