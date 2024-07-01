package me.kes.magicalchat;

import lombok.RequiredArgsConstructor;
import org.bukkit.ChatColor;
import org.bukkit.entity.Player;
import org.bukkit.event.EventHandler;
import org.bukkit.event.Listener;
import org.bukkit.event.player.AsyncPlayerChatEvent;
import org.bukkit.event.player.PlayerQuitEvent;
import java.util.HashMap;
import java.util.Map;

@RequiredArgsConstructor
public class ChatCooldown implements Listener {
    public final MagicalChat mainplugin;
    private final Map<Player, Long> lastChat = new HashMap<>();

    @EventHandler
    public void onPlayerChat(AsyncPlayerChatEvent event) {
        Player player = event.getPlayer();
        long currentTime = System.currentTimeMillis();
        float cooldown;

        if (player.hasPermission("group.helper")){
            return;
        }

        // Check if the player has chatted within the last 3 seconds
        if (!(player.hasPermission("chatcooldown.bypass"))) {
            if (lastChat.containsKey(player) && currentTime - lastChat.get(player) < 3000) {
                cooldown = (float) (3000 - (currentTime - lastChat.get(player))) / 1000;
                event.setCancelled(true);
                player.sendMessage(ChatColor.RED + "Please wait " + cooldown + " seconds before chatting again");
                return;
            }
        }

        if (lastChat.containsKey(player) && currentTime - lastChat.get(player) < 1500) {
            cooldown = (float) (1500 - (currentTime - lastChat.get(player))) / 1000;
            event.setCancelled(true);
            player.sendMessage(ChatColor.RED + "Please wait " + cooldown + " seconds before chatting again");
            return;
        }

        // Update the last chat time for the player
        lastChat.put(player, currentTime);
    }

    @EventHandler
    public void onPlayerQuit(PlayerQuitEvent event){
        lastChat.remove(event.getPlayer());
    }
}
