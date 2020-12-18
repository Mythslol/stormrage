/*
 * This file is part of the CMaNGOS Project. See AUTHORS file for Copyright information
 *
 * This program is free software; you can redistribute it and/or modify
 * it under the terms of the GNU General Public License as published by
 * the Free Software Foundation; either version 2 of the License, or
 * (at your option) any later version.
 *
 * This program is distributed in the hope that it will be useful,
 * but WITHOUT ANY WARRANTY; without even the implied warranty of
 * MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 * GNU General Public License for more details.
 *
 * You should have received a copy of the GNU General Public License
 * along with this program; if not, write to the Free Software
 * Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA  02111-1307  USA
 */

#include "Common.h"
#include "Database/DatabaseEnv.h"
#include "World/World.h"
#include "Entities/Player.h"
#include "Server/Opcodes.h"
#include "Chat/Chat.h"
#include "Globals/ObjectAccessor.h"
#include "Tools/Language.h"
#include "Accounts/AccountMgr.h"
#include "AI/ScriptDevAI/ScriptDevAIMgr.h"
#include "SystemConfig.h"
#include "revision.h"
#include "Util.h"

bool ChatHandler::HandleCustomAnn(char* args)
{
  int32 strid = 0;

    if(!*args)
        return false;

    switch(m_session->GetSecurity()) {
      case SEC_ADMINISTRATOR:
        strid = LANG_SYSTEMMESSAGE_ADMINISTRATOR; //LANG_SYSTEMMESSAGE_ADMINISTRATOR odkazuje z language.h
        break;
      default:
        return false;
    }

    sWorld.SendWorldText(strid, m_session->GetPlayerName(), args);

    return true;
}
// VIP COMMANDS

	//Bank
bool ChatHandler::HandleVipBankCommand(char* /*args*/)
{
	Player * pl = m_session->GetPlayer();
        if(pl->IsInCombat())
        {
            pl->GetSession()->SendNotification("You can't use this in combat!");
            return false;
        }
		else
		m_session->SendShowBank(m_session->GetPlayer()->GetObjectGuid());

    return true;
}
	//Auction
bool ChatHandler::HandleVipAuctionAllianceCommand(char* /*args*/)
{
    m_session->GetPlayer()->SetAuctionAccessMode(m_session->GetPlayer()->GetTeam() != ALLIANCE ? -1 : 0);
    m_session->SendAuctionHello(m_session->GetPlayer());
    return true;
}

bool ChatHandler::HandleVipAuctionHordeCommand(char* /*args*/)
{
    m_session->GetPlayer()->SetAuctionAccessMode(m_session->GetPlayer()->GetTeam() != HORDE ? -1 : 0);
    m_session->SendAuctionHello(m_session->GetPlayer());
    return true;
}

bool ChatHandler::HandleVipAuctionGoblinCommand(char* /*args*/)
{
    m_session->GetPlayer()->SetAuctionAccessMode(1);
    m_session->SendAuctionHello(m_session->GetPlayer());
    return true;
}

bool ChatHandler::HandleVipAuctionCommand(char* /*args*/)
{
    m_session->GetPlayer()->SetAuctionAccessMode(0);
    m_session->SendAuctionHello(m_session->GetPlayer());

    return true;
}

	//Repair
bool ChatHandler::HandleVipRepairitemsCommand(char* args)
{
	Player * pl = m_session->GetPlayer();
        if(pl->IsInCombat())
        {
            pl->GetSession()->SendNotification("You can't use this in combat!");
            return false;
        }
		else
		// Repair items
		m_session->GetPlayer()->DurabilityRepairAll(false, 0, false);
		PSendSysMessage("Your items are repaired");
		return true;

}

bool ChatHandler::HandleBuffCommand(char * args)
    {
        Player * pl = m_session->GetPlayer();
        if(pl->IsInCombat())
        {
            pl->GetSession()->SendNotification("You can't use this in combat!");
            return false;
        }
        if(pl->InArena())
        {
            pl->GetSession()->SendNotification("You can't use that item in an arena match!");
            return false;
        }
        else
        pl->CastSpell(pl, 36880, TRIGGERED_OLD_TRIGGERED);
        pl->CastSpell(pl, 467, TRIGGERED_OLD_TRIGGERED);
        PSendSysMessage("You have been buffed, enjoy!");
        return true;
 
    }
