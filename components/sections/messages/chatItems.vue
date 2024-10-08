<template>
  <div ref="el" class="chat-items">
    <SectionsMessagesChatItem
      v-for="item in messagesStore.chats.filter((chat) =>
        chat.members.some((member) => member._id === userStore?.user?._id),
      )"
      :key="item._id"
      class="chat-item"
      :chat="item"
      @click="selectChat(item)"
    ></SectionsMessagesChatItem>
  </div>
</template>
<script setup lang="ts">
import type { ChatListItem } from "~/types/messages.types";
const el = ref<HTMLElement | null>(null);
const route = useRoute();

useInfiniteScroll(el, loadChats, {
  distance: 100,
  interval: 5000,
  direction: "bottom",
  canLoadMore: () => {
    return (
      messagesStore.totalCountChats > messagesStore.chats.length &&
      messagesStore.chats.length >= messagesStore.limit
    );
  },
});

const props = defineProps<{ chosen: "orders" | "chats" }>();
const messagesStore = useMessagesStore();
const userStore = useUserStore();
function selectChat(respondent: ChatListItem) {
  if (messagesStore.activeChat?._id === respondent._id) return;
  messagesStore.resetMessages();
  messagesStore.activeChat = respondent;
  const router = useRouter();
  router.push({ query: { id: respondent._id, tab: props.chosen } });
  messagesStore.fetchChatMessagesList({
    chat_id: messagesStore.activeChat?._id,
    offset: messagesStore.messagesListOffset,
    limit: messagesStore.limit,
  });
}

async function loadChats() {
  messagesStore.chatListOffset += 1;
  const queryParams = {
    limit: messagesStore.limit,
    offset: messagesStore.chatListOffset,
    search: messagesStore.searchQuery,
  };
  if (props.chosen === "chats") await messagesStore.fetchChats(queryParams);
  else if (props.chosen === "orders")
    await messagesStore.fetchOrdersChats(queryParams);
}

if (props.chosen === "chats")
  await messagesStore.fetchChats({
    limit: messagesStore.limit,
    offset: 1,
  });
else if (props.chosen === "orders")
  await messagesStore.fetchOrdersChats({
    limit: messagesStore.limit,
    offset: 1,
  });

if (route.query?.id) {
  messagesStore.activeChat = messagesStore.chats.find(
    (item) => item._id === route.query?.id,
  );

  if (messagesStore.activeChat)
    messagesStore.fetchChatMessagesList({
      chat_id: messagesStore.activeChat._id,
      offset: messagesStore.messagesListOffset,
    });
}
</script>
