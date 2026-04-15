# CRD Domain Model

This diagram represents the current CRD model and semantic relationships used by `krun`.

```mermaid
classDiagram
    class AnsibleTask {
      +metadata.name: string
      +spec.action: string
      +spec.args: object?
      +spec.when: string?
      +spec.tags: string[]?
      +status.conditions[]
    }

    class BlockTaskRef {
      +id: string
      +task: string
    }

    class AnsibleBlock {
      +metadata.name: string
      +spec.block: BlockTaskRef[1..*]
      +spec.rescue: BlockTaskRef[0..*]
      +spec.always: BlockTaskRef[0..*]
      +status.conditions[]
    }

    class RoleEntryRef {
      +id: string
      +task: string?  
      +block: string?
      +constraint: exactly one of task or block
    }

    class AnsibleRole {
      +metadata.name: string
      +spec.preTasks: RoleEntryRef[0..*]
      +spec.tasks: RoleEntryRef[1..*]
      +spec.postTasks: RoleEntryRef[0..*]
      +spec.handlers: RoleEntryRef[0..*]
      +status.conditions[]
    }

    AnsibleBlock "1" *-- "1..*" BlockTaskRef : block
    AnsibleBlock "1" *-- "0..*" BlockTaskRef : rescue
    AnsibleBlock "1" *-- "0..*" BlockTaskRef : always
    BlockTaskRef --> AnsibleTask : references by metadata.name

    AnsibleRole "1" *-- "0..*" RoleEntryRef : preTasks
    AnsibleRole "1" *-- "1..*" RoleEntryRef : tasks
    AnsibleRole "1" *-- "0..*" RoleEntryRef : postTasks
    AnsibleRole "1" *-- "0..*" RoleEntryRef : handlers

    RoleEntryRef --> AnsibleTask : task reference (optional)
    RoleEntryRef --> AnsibleBlock : block reference (optional)
```

## Notes

- All resources are namespaced.
- `RoleEntryRef` uses a union constraint: exactly one of `task` or `block`.
- `AnsibleRole` may reference `AnsibleBlock`; `AnsibleBlock` references `AnsibleTask`.
