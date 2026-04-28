# When to use Breadcrumb

Use a breadcrumb when the user is more than two levels deep in
content hierarchy and the parent context is not visible elsewhere
(sidebar, page header). Skip the breadcrumb when the parent is
already in the sidebar — duplicating navigation surface adds cost
without adding clarity.

The current page is the last item, marked `aria-current="page"`,
and is not a link.
