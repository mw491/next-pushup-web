<script lang="ts">
  import { onMount } from "svelte";

  let latestRelease: string = "";
  let downloadUrl: string = "";

  onMount(async () => {
    try {
      const response = await fetch(
        "https://api.github.com/repos/mw491/next-pushup/releases/latest",
      );
      const data = await response.json();
      latestRelease = data.tag_name;
      downloadUrl =
        data.assets[0]?.browser_download_url ||
        "https://github.com/mw491/next-pushup/releases";
    } catch (error) {
      console.error("Error fetching release:", error);
      downloadUrl = "https://github.com/mw491/next-pushup/releases";
    }
  });
</script>

<svelte:head>
  <title>NEXT PUSHUP - Transform Your Pushup Game</title>
  <meta
    name="description"
    content="Track and improve your pushup performance with NEXT PUSHUP. Set goals, monitor progress, and get daily reminders for consistent training."
  />
  <meta
    name="keywords"
    content="pushup tracker, fitness app, workout tracker, exercise goals"
  />
  <meta
    property="og:title"
    content="NEXT PUSHUP - Transform Your Pushup Game"
  />
  <meta
    property="og:description"
    content="Track and improve your pushup performance with NEXT PUSHUP."
  />
  <meta property="og:type" content="website" />
</svelte:head>

<main class="min-h-screen bg-np-dark">
  <div class="max-w-7xl mx-auto px-4 py-32 sm:px-6 lg:px-8">
    <!-- Hero Section -->
    <section class="text-center mb-16 animate-fade-in">
      <h1 class="text-4xl sm:text-6xl mb-4">NEXT PUSHUP</h1>
      <p class="text-xl sm:text-2xl mb-8 text-gray-300">
        Transform your pushup game to the next level
      </p>

      <div class="flex justify-center gap-4 mb-12">
        <a href={downloadUrl} class="btn-primary">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-6 w-6"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4"
            />
          </svg>
          Download Now {latestRelease && `(${latestRelease})`}
        </a>
        <a href="https://github.com/mw491/next-pushup" class="btn-primary">
          View on GitHub
        </a>
      </div>
    </section>

    <!-- App Preview and Features Section -->
    <section class="md:flex md:gap-12 md:items-center md:justify-center mb-16">
      <!-- App Screenshot -->
      <div class="md:w-1/2 mb-12 md:mb-0">
        <div class="max-w-sm mx-auto md:max-w-none">
          <img
            src="/app-screenshot.jpg"
            alt="NEXT PUSHUP App Interface"
            class="rounded-2xl shadow-2xl max-w-sm shadow-black"
            loading="lazy"
          />
        </div>
      </div>

      <!-- Features List -->
      <div class="md:w-1/3">
        <div class="grid gap-6">
          <div
            class="bg-np-gray p-6 rounded-xl transform transition-transform hover:scale-105"
          >
            <h3 class="text-xl mb-4 flex items-center gap-2">
              📊 Track Daily Sets
            </h3>
            <p class="text-gray-300">
              Keep track of your pushup sets with a simple, intuitive interface
            </p>
          </div>

          <div
            class="bg-np-gray p-6 rounded-xl transform transition-transform hover:scale-105"
          >
            <h3 class="text-xl mb-4 flex items-center gap-2">🎯 Set Goals</h3>
            <p class="text-gray-300">Set and monitor your daily pushup goals</p>
          </div>

          <div
            class="bg-np-gray p-6 rounded-xl transform transition-transform hover:scale-105"
          >
            <h3 class="text-xl mb-4 flex items-center gap-2">
              📈 View Statistics
            </h3>
            <p class="text-gray-300">
              Track your progress with detailed statistics
            </p>
          </div>

          <div
            class="bg-np-gray p-6 rounded-xl transform transition-transform hover:scale-105"
          >
            <h3 class="text-xl mb-4 flex items-center gap-2">
              🔔 Daily Reminders
            </h3>
            <p class="text-gray-300">
              Stay consistent with customizable reminders
            </p>
          </div>
        </div>
      </div>
    </section>
  </div>
</main>
