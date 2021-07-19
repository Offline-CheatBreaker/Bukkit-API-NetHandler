```java
    public boolean sendPacket(Player player, CBPacket packet) {
        if (isRunningCheatBreaker(player)) {
            player.sendPluginMessage(this, CB_MESSAGE_CHANNEL, CBPacket.getPacketData(packet));
            Bukkit.getPluginManager().callEvent(new CBPacketSentEvent(player, packet));
            return true;
        } else if (!playersNotRegistered.contains(player.getUniqueId())) {
            cbPacketQueue.putIfAbsent(player.getUniqueId(), new ArrayList<>());
            cbPacketQueue.get(player.getUniqueId()).add(packet);
            return false;
        }
        return false;
    }
```
