// Component for selecting predefined AI instructions

Component QuickPrompts(onSelect) {
    Constants prompts = [
        "Simplify language for patient readability",
        "Add plain-language summary"
    ]

    Render {
        List {
            prompts.map(p => (
                Button(label=p, onClick={() => onSelect(p)})
            ))
        }
    }
}