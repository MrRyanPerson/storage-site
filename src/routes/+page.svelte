<script>
    import { resolve } from '$app/paths';
</script>

<div class="min-h-screen flex items-center justify-center">
  <div class="h-80 grid grid-cols-2 gap-4 place-content-center">
    <a href="{resolve('/download')}" class="bg-gray-200 p-4 rounded-md flex flex-col items-center gap-2 cursor-pointer hover:bg-gray-300">
        <svg xmlns="http://www.w3.org/2000/svg" height="48px" viewBox="0 -960 960 960" width="48px" fill="#181818"><path d="M140-160q-24.75 0-42.37-17.63Q80-195.25 80-220v-440q0-24.75 17.63-42.38Q115.25-720 140-720h254l80-80h346q24.75 0 42.38 17.62Q880-764.75 880-740v520q0 24.75-17.62 42.37Q844.75-160 820-160H140Zm59-280h241v-241L199-440Zm-59-26 194-194H140v194Zm0 86v160h680v-520H500v300q0 24.75-17.62 42.37Q464.75-380 440-380H140Zm310-130Z"/></svg>
        <p class="font-semibold">Download Files</p>
    </a>
    <a href="{resolve('/upload')}" class="bg-gray-200 p-4 rounded-md flex flex-col items-center gap-2 cursor-pointer hover:bg-gray-300">
        <svg xmlns="http://www.w3.org/2000/svg" height="48px" viewBox="0 -960 960 960" width="48px" fill="#181818"><path d="M250-160q-86 0-148-62T40-370q0-78 49.5-137.5T217-579q20-97 94-158.5T482-799q113 0 189.5 81.5T748-522v24q72-2 122 46.5T920-329q0 69-50 119t-119 50H510q-24 0-42-18t-18-42v-258l-83 83-43-43 156-156 156 156-43 43-83-83v258h241q45 0 77-32t32-77q0-45-32-77t-77-32h-63v-84q0-89-60.5-153T478-739q-89 0-150 64t-61 153h-19q-62 0-105 43.5T100-371q0 62 43.93 106.5T250-220h140v60H250Zm230-290Z"/></svg>
        <p href="{resolve('/upload')}" class="font-semibold">Upload Files</p>
    </a>
  </div>
</div>
