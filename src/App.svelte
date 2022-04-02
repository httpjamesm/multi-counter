<script lang="ts">

    import { Router, Route } from "svelte-routing";

    import Dexie from "dexie";
    
    import Home from "./pages/Home.svelte";
    import Counter from "./pages/Counter.svelte";

    if (!window.indexedDB) {
        alert("IndexedDB is unsupported in this browser.");
    }

    const db: Dexie = new Dexie("SimpleCounter");

    db.version(1).stores({
        counters: "++id, name, description, color, count"
    });

    db.open().catch(function(e) {
        alert("Open failed: " + e);
    });

</script>

<Router>
    <Route path="/">
        <Home db={db} />
    </Route>
    <Route path="counter">
        <Counter 
            db={db}
         />
    </Route>
</Router>