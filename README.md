Role Name
=========

A brief description of the role goes here.

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).

```
memory used [in bytes] = gpu_runners_per_device * chunks_per_runner * chunk_size * model_factor



Where model_factor depends on the basecall model used:

Basecall model	model_factor
Fast	1200
HAC	3300
SUP	12600
Note that gpu_runners_per_device is a limit setting. Guppy will create at least one runner per device and will dynamically increase this number as needed up to gpu_runners_per_device. Performance is usually much better with multiple runners, so it is important to choose parameters such that chunks_per_runner * chunk_size * model_factor is less than half the total GPU memory available. If this value is more than the available GPU memory, Guppy will exit with an error.

For example, when basecalling using a SUP model and a chunk size of 2000 on a GPU with 8 GB of memory, we have to make sure that the GPU can fit at least one runner:


chunks_per_runner * chunk_size * model_factor should be lower than GPU memory
chunks_per_runner * 2000 * 12600 should be lower than 8 GB
chunks_per_runner lower than ~340

This represents the limit beyond which Guppy will not run at all. For best performance we recommend using an integer fraction of this number, rounded down to an even number, e.g. a third (~112) or a quarter (~84). Especially for fast models, it can be best to have a dozen runners or more. The ideal value varies depending on GPU architecture and available memory.
```