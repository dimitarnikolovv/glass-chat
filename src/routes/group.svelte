<script>
    import Filter from 'bad-words';
    import { groupes } from '../stores/group';
    import router from 'page';

    function groupSubmit(e) {
        if (e.key.toLowerCase() !== 'enter') return;

        const group = new Filter().clean(
            (document.getElementById('group-input').value || '').trim()
        );

        if (!group) return;

        document.getElementById('group-input').value = '';

        if (localStorage.getItem('group') === group.toLowerCase()) {
            router.redirect('/chat');
            return;
        }

        localStorage.setItem('group', group.toLowerCase());

        $groupes = group.toLowerCase();

        setTimeout(() => {
            router.redirect('/chat');
        }, 200);
    }
</script>

<h1 class="w3-jumbo w3-center">Choose or create group</h1>

<input
    on:keydown={groupSubmit}
    type="text"
    style="margin: 0 auto; width: 60%; margin-top: -1px"
    class="w3-input w3-border w3-border-gray"
    id="group-input"
/>
