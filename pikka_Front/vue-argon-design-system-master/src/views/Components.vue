<template>
  <div>
    <Sildcompoent></Sildcompoent>
    <announcementcompoent></announcementcompoent>
    <cardcompoent></cardcompoent>
    <cardcompoent2></cardcompoent2>
  </div>
</template>
<script>
import Sildcompoent from "./components/Sildcompoent";
import announcementcompoent from "./components/announcementcompoent";
import cardcompoent from "./components/cardcompoent";
import cardcompoent2 from "./components/cardcompoent2";

export default {
  name: "components",
  components: {
    Sildcompoent,
    announcementcompoent,
    cardcompoent,
    cardcompoent2
  },
};
</script>
