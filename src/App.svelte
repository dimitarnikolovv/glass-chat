<script>
    import router from 'page';
    import Auth from './routes/auth.svelte';
    import Index from './routes/index.svelte';
    import Chat from './routes/chat.svelte';
    import Group from './routes/group.svelte';
    import NotFound from './routes/notfound.svelte';
    import { queryString } from './services/util';
    import { groupes } from './stores/group';

    if (localStorage.getItem('group')) {
        $groupes = localStorage.getItem('group');
    }

    let page;
    let params = {};
    let qs = {};

    router('/', () => (page = Index));
    router(
        '/404/:msg',
        (ctx = { params: {}, querystring: string }, next) => {
            params = ctx.params;
            next();
        },
        () => (page = NotFound)
    );
    router(
        '/auth',
        (ctx, next) => {
            qs = queryString(ctx.querystring);
            next();
        },
        () => (page = Auth)
    );
    router('/login', () => router.redirect('/auth'));
    router('/register', () => router.redirect('/auth'));
    router('/chat', () => (page = Chat));
    router('/group', () => (page = Group));

    router('/*', () => (page = NotFound));
    router.start();
</script>

<svelte:component this={page} {params} {qs} />
