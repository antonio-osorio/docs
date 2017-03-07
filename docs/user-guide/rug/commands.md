Controlling communication and information flows is paramount to
effective teams.  Open Source projects have long been relying on chat
to help them operate and coordinate.  Recent modern chat solutions,
which can integrate deeply in your ecosystem, have proven to be
fantastic hubs for teams to communicate and drive their workflows.

Rug commands provide a simple interface to add new skills to the
Atomist Bot.

## A Basic Command

The following command responds to commands passed to the Atomist bot,
`@atomist add markdown-document`.  The handler calls
our [editor](editors.md), but could also make externals calls, and
responds with a message.

```typescript
import { HandleCommand, Plan } from '@atomist/rug/operations/Handlers'
import { CommandHandler, Parameter, Tags, Intent } from '@atomist/rug/operations/Decorators'
import { Project } from '@atomist/rug/model/Core'

@CommandHandler("AddMarkdownDocument","Runs the SetLicense editor on a bunch of my repos")
@Tags("markdown", "documentation")
@Intent("add markdown-document")
class AddMarkdownDocument implements HandleCommand {

    @Parameter({description: "name of your new document", pattern: Pattern.any})
    docname: string

    @Parameter({description: "document's top-level title", pattern: Pattern.any})
    title: string

    @Parameter({description: "document's default content", pattern: Pattern.any})
    content: string

    handle(command: HandlerContext) : Plan {
        let result = new Plan()
        result.add(new Message("Added!"))
        return result;
    }
}
export const addMarkdownDocument = new AddMarkdownDocument();
```