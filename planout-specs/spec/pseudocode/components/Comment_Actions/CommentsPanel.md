component CommentsPanel(documentId: string) {
    // Node: Comments (d63dab83-693f-45c8-9bf2-6c861409fdc3)
    
    state comments = [];
    
    onMount(() => {
        comments = API.fetchComments(documentId);
    });

    onUnmount(() => {
        API.cancelPendingRequests();
        comments = [];
    });

    render() {
        return (
            <ScrollableList>
                {comments.map(comment => (
                    <CommentCard key={comment.id} data={comment} />
                ))}
                <AddCommentComposer />
            </ScrollableList>
        );
    }
}
// Notes covered: Scrollable threaded list, Surfaces section label/avatar/name/time/body, Status toggle (Open/Resolved/Closed), Reply button with count, Inline reply form with auto-focus, Nested replies as compact sub-items.