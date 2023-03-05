<script>
  import Button from "./lib/button.svelte";
  import { Router, Link, Route } from "svelte-navigator";
  import Chat from "./lib/Chat.svelte";
  import Contact from "./lib/Contact.svelte";

  $: filterFun = (e) => {
    show(e.detail.click);
  };

  const show = (data) => {
    alert(`clicked on ${data === "Chat" ? "Chat" : "Contact"}`);
    const fileName = "MyAppUl.js";
    const fileContent = `MyAppUI. show ((screen: '${data}', data:{ "message": "${
      data === "Chat" ? "Hello" : "Hi"
    }"}H):`;

    const blob = new Blob([fileContent], { type: "text/javascript" });
    const link = document.createElement("a");
    link.href = window.URL.createObjectURL(blob);
    link.download = fileName;
    link.click();
  };
</script>

<main>
  <Router>
    <nav class="flex my-5 w-full justify-center items-center gap-5">
      <Link to="/chat">
        <Button title="Chat" on:filterFun={filterFun} />
      </Link>
      <Link to="/contact">
        <Button title="Contact" on:filterFun={filterFun} />
      </Link>
    </nav>
    <div class="border h-[400px] rounded-lg m-5 p-5">
      <Route path="/chat" component={Chat} callFunt="contact" />
      <Route path="/contact" component={Contact} />
    </div>
  </Router>
</main>
