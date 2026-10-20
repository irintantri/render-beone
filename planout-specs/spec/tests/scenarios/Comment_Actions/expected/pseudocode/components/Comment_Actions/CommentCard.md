// Individual comment thread component
Component CommentCard(comment):
    Render:
        SectionLabel(comment.section)
        AuthorInfo(comment.author.avatar, comment.author.name, comment.timestamp)
        CommentBody(comment.text)
        
        StatusToggle(comment.status):
            OnChange(newStatus) -> API.updateCommentStatus(comment.id, newStatus)
        
        ReplySection:
            ReplyCount(comment.replies.length)
            Button("Reply") -> Toggle(isReplying)
            If isReplying:
                InlineReplyForm(parentId: comment.id)